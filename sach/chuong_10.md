Bài toán đề ra là giải phương trình vi phân cấp hai sau:

$$
\varepsilon \bar{y}'' + \bar{y}' + \bar{y} = 1, \quad \bar{y}(0) = 0, \quad \bar{y}'(0) = 1,
$$

với $\varepsilon = 0.01$, từ $t=0$ đến $t=1$ bằng nhiều phương pháp số khác nhau (Explicit Euler, Implicit Euler, Implicit Trapezoid, Modified Euler, Gear các bậc).

---

## 1. Chuyển đổi bài toán về hệ phương trình bậc nhất

Đặt:

$$
y_1 = \bar{y}, \quad y_2 = \bar{y}',
$$

khi đó:

$$
y_1' = y_2,
$$

$$
\varepsilon y_2' + y_2 + y_1 = 1 \implies y_2' = \frac{1 - y_2 - y_1}{\varepsilon}.
$$

Ta có hệ:

$$
\begin{cases}
y_1' = y_2, \\
y_2' = \frac{1 - y_2 - y_1}{\varepsilon},
\end{cases}
$$

với điều kiện ban đầu:

$$
y_1(0) = 0, \quad y_2(0) = 1.
$$

---

## 2. Các phương pháp giải

Bạn cần giải hệ trên từ $t=0$ đến $t=1$ với các phương pháp:

* Explicit Euler (Bài 213),
* Implicit Euler (Bài 214),
* Implicit Trapezoid (Bài 215),
* Modified Euler (Bài 216),
* Gear bậc 1 (Bài 217),
* Gear bậc 2 (Bài 218),
* Gear bậc 4 (Bài 219).

Mỗi phương pháp có các bước thời gian $\Delta t$ khác nhau như đề bài.

---

## 3. Ví dụ: giải bằng phương pháp Explicit Euler

Công thức Explicit Euler với bước $\Delta t$:

$$
y_{n+1} = y_n + \Delta t \cdot f(t_n, y_n)
$$

Ở đây $y_n = (y_{1,n}, y_{2,n})$, $f(t,y) = (y_2, \frac{1 - y_2 - y_1}{\varepsilon})$.

**Thuật toán:**

* Khởi tạo: $y_1(0) = 0$, $y_2(0) = 1$.
* Với mỗi bước $n$:

  $$
  y_{1,n+1} = y_{1,n} + \Delta t \cdot y_{2,n}
  $$

  $$
  y_{2,n+1} = y_{2,n} + \Delta t \cdot \frac{1 - y_{2,n} - y_{1,n}}{\varepsilon}
  $$
* Lặp đến $t = 1$.

---

## 4. Cách triển khai các phương pháp khác

* **Implicit Euler:**

$$
y_{n+1} = y_n + \Delta t \cdot f(t_{n+1}, y_{n+1}),
$$

phải giải hệ phương trình để tìm $y_{n+1}$.

* **Implicit Trapezoid:**

$$
y_{n+1} = y_n + \frac{\Delta t}{2}[f(t_n,y_n) + f(t_{n+1}, y_{n+1})],
$$

phải giải hệ phương trình phi tuyến với $y_{n+1}$.

* **Modified Euler:** là phương pháp cải tiến từ explicit Euler, thường liên quan trung bình hóa dốc.

* **Gear method:** là phương pháp đa bước, cần giá trị bắt đầu từ các phương pháp bậc thấp hơn.

---

## 5. Gợi ý triển khai

Bạn có thể triển khai giải trong Python, Matlab hoặc phần mềm khác, ví dụ với Python:

```python
import numpy as np

def f(y, eps):
    y1, y2 = y
    dy1 = y2
    dy2 = (1 - y2 - y1)/eps
    return np.array([dy1, dy2])

def explicit_euler(y0, t0, t_end, dt, eps):
    t = t0
    y = y0
    results = [(t, y.copy())]
    while t < t_end:
        y = y + dt * f(y, eps)
        t += dt
        results.append((t, y.copy()))
    return results

eps = 0.01
y0 = np.array([0.0, 1.0])
dt = 0.01
res = explicit_euler(y0, 0.0, 1.0, dt, eps)
for t, y in res:
    print(f"t={t:.2f}, y={y[0]:.5f}, y'={y[1]:.5f}")
```

---

Nếu bạn muốn tôi hỗ trợ giải cụ thể bằng một phương pháp nào, hoặc triển khai code cụ thể, bạn vui lòng cho biết nhé!

