Dưới đây mình sẽ hướng dẫn chi tiết cách giải bài toán từ câu 213 đến 218 theo từng phương pháp, với hệ ODE đã chuyển thành hệ 2 phương trình bậc nhất:

$$
\begin{cases}
y_1' = y_2, \\
y_2' = \frac{1 - y_2 - y_1}{\varepsilon},
\end{cases}
\quad y_1(0) = 0, \quad y_2(0) = 1, \quad \varepsilon = 0.01,
$$

trên đoạn $t \in [0,1]$.

---

# 213. Giải bằng phương pháp **Explicit Euler**

* Bước thời gian: $\Delta t = 0.01, 0.02, 0.025$
* Công thức cập nhật:

$$
\begin{cases}
y_{1,n+1} = y_{1,n} + \Delta t \cdot y_{2,n}, \\
y_{2,n+1} = y_{2,n} + \Delta t \cdot \frac{1 - y_{2,n} - y_{1,n}}{\varepsilon}.
\end{cases}
$$

* Khởi tạo: $y_{1,0} = 0, y_{2,0} = 1, t_0 = 0$.
* Lặp đến $t_n = 1$.

---

# 214. Giải bằng phương pháp **Implicit Euler**

* Bước thời gian: $\Delta t = 0.1, 0.2, 0.25$
* Công thức cập nhật ẩn (implicit):

$$
\begin{cases}
y_{1,n+1} = y_{1,n} + \Delta t \cdot y_{2,n+1}, \\
y_{2,n+1} = y_{2,n} + \Delta t \cdot \frac{1 - y_{2,n+1} - y_{1,n+1}}{\varepsilon}.
\end{cases}
$$

* $y_{n+1} = (y_{1,n+1}, y_{2,n+1})$ phải được giải từ hệ phương trình tuyến tính:

$$
\begin{cases}
y_{1,n+1} - \Delta t y_{2,n+1} = y_{1,n}, \\
y_{2,n+1} + \frac{\Delta t}{\varepsilon} y_{2,n+1} + \frac{\Delta t}{\varepsilon} y_{1,n+1} = y_{2,n} + \frac{\Delta t}{\varepsilon}.
\end{cases}
$$

Ta có thể viết lại dưới dạng ma trận:

$$
\begin{bmatrix}
1 & -\Delta t \\
\frac{\Delta t}{\varepsilon} & 1 + \frac{\Delta t}{\varepsilon}
\end{bmatrix}
\begin{bmatrix}
y_{1,n+1} \\
y_{2,n+1}
\end{bmatrix}
=
\begin{bmatrix}
y_{1,n} \\
y_{2,n} + \frac{\Delta t}{\varepsilon}
\end{bmatrix}.
$$

Giải hệ trên để tìm $y_{1,n+1}, y_{2,n+1}$.

---

# 215. Giải bằng phương pháp **Implicit trapezoid**

* Bước thời gian: $\Delta t = 0.1, 0.2, 0.25$
* Công thức:

$$
y_{n+1} = y_n + \frac{\Delta t}{2} [f(t_n, y_n) + f(t_{n+1}, y_{n+1})].
$$

Chi tiết cho từng thành phần:

$$
\begin{cases}
y_{1,n+1} = y_{1,n} + \frac{\Delta t}{2} (y_{2,n} + y_{2,n+1}), \\
y_{2,n+1} = y_{2,n} + \frac{\Delta t}{2} \left( \frac{1 - y_{2,n} - y_{1,n}}{\varepsilon} + \frac{1 - y_{2,n+1} - y_{1,n+1}}{\varepsilon} \right).
\end{cases}
$$

Viết lại:

$$
\begin{cases}
y_{1,n+1} - \frac{\Delta t}{2} y_{2,n+1} = y_{1,n} + \frac{\Delta t}{2} y_{2,n}, \\
y_{2,n+1} + \frac{\Delta t}{2\varepsilon} y_{2,n+1} + \frac{\Delta t}{2\varepsilon} y_{1,n+1} = y_{2,n} + \frac{\Delta t}{2\varepsilon} (1 - y_{2,n} - y_{1,n}) + \frac{\Delta t}{2\varepsilon}.
\end{cases}
$$

Cũng là hệ phương trình tuyến tính để giải cho $y_{1,n+1}, y_{2,n+1}$.

---

# 216. Giải bằng phương pháp **Modified Euler** (Heun’s method)

* Bước thời gian: $\Delta t = 0.01, 0.02, 0.025$
* Bước 1: Tính $k_1 = f(t_n, y_n)$
* Bước 2: Tính $y^* = y_n + \Delta t \cdot k_1$ (dự báo bằng Explicit Euler)
* Bước 3: Tính $k_2 = f(t_{n+1}, y^*)$
* Bước 4: Cập nhật:

$$
y_{n+1} = y_n + \frac{\Delta t}{2} (k_1 + k_2).
$$

Áp dụng cho từng thành phần:

$$
k_1 = \begin{bmatrix} y_{2,n} \\ \frac{1 - y_{2,n} - y_{1,n}}{\varepsilon} \end{bmatrix}, \quad
y^* = y_n + \Delta t k_1,
$$

$$
k_2 = \begin{bmatrix} y_2^* \\ \frac{1 - y_2^* - y_1^*}{\varepsilon} \end{bmatrix}.
$$

---

# 217. Giải bằng **Gear phương pháp bậc nhất**

* Bước thời gian: $\Delta t = 0.1, 0.2$
* Gear bậc nhất tương tự phương pháp backward Euler, công thức:

$$
y_{n+1} = y_n + \Delta t f(t_{n+1}, y_{n+1}),
$$

giải hệ phương trình ẩn giống câu 214 (Implicit Euler).

---

# 218. Giải bằng **Gear phương pháp bậc hai**

* Bước thời gian: $\Delta t = 0.1$
* Dùng giá trị bắt đầu từ phương pháp Gear bậc nhất.
* Công thức Gear bậc hai:

$$
\frac{1}{\Delta t^2} (y_{n+1} - 2 y_n + y_{n-1}) = f'(t_{n+1}, y_{n+1}),
$$

với $f'$ là đạo hàm theo thời gian (hoặc dạng xấp xỉ).

Phương pháp này phức tạp hơn, thường được áp dụng cho bài toán có đạo hàm cấp cao. Trong thực tế, Gear bậc hai được dùng trong giải tích số cho hệ phương trình vi phân cứng.

---

# Tóm tắt:

| Câu | Phương pháp                    | Bước thời gian $\Delta t$ | Cách giải chính                                                                  |
| --- | ------------------------------ | ------------------------- | -------------------------------------------------------------------------------- |
| 213 | Explicit Euler                 | 0.01, 0.02, 0.025         | Cập nhật $y_{n+1} = y_n + \Delta t f(t_n,y_n)$                                   |
| 214 | Implicit Euler                 | 0.1, 0.2, 0.25            | Giải hệ $y_{n+1} = y_n + \Delta t f(t_{n+1}, y_{n+1})$                           |
| 215 | Implicit trapezoid             | 0.1, 0.2, 0.25            | Giải hệ với $y_{n+1} = y_n + \frac{\Delta t}{2}[f(t_n,y_n)+f(t_{n+1}, y_{n+1})]$ |
| 216 | Modified Euler (Heun)          | 0.01, 0.02, 0.025         | Dự báo explicit Euler, sau đó trung bình dốc $k_1,k_2$                           |
| 217 | Gear bậc nhất (Backward Euler) | 0.1, 0.2                  | Giống implicit Euler                                                             |
| 218 | Gear bậc hai                   | 0.1                       | Dùng giá trị bắt đầu từ Gear 1, công thức Gear 2 (đa bước)                       |

---

Nếu bạn muốn, mình có thể giúp bạn viết code cụ thể cho từng phương pháp, hoặc tính toán từng bước mẫu. Bạn muốn mình làm bước nào trước?
