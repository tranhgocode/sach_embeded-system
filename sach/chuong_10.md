### Độ mặn dọc theo trục sông‑biển không phải lúc nào cũng “thẳng” 

Khi nước ngọt của sông pha trộn với nước mặn của biển trong cửa sông (estuary), phân bố độ mặn $S(x)$ theo khoảng cách $x$ từ cửa biển phụ thuộc đồng thời vào:

| Thành phần chi phối                         | Ví dụ tác động                                                                             |
| ------------------------------------------- | ------------------------------------------------------------------------------------------ |
| *Lưu lượng sông $(Q_r)$*                  | Dòng lớn đẩy giới hạn nhiễm mặn ra ngoài khơi; dòng cạn cho phép mặn xâm nhập sâu.         |
| *Cường độ triều & khuấy trộn*             | Triều mạnh → cửa sông “well‑mixed”, grad $S$ nhỏ; triều yếu → hình thành “salt‑wedge” dốc. |
| *Hình học kênh (hội tụ, độ sâu, bề rộng)* | Kênh loe dần ra biển thường làm đường cong $S(x)$ lồi, gần hàm mũ.                         |
| *Gió, Coriolis, uốn cong kênh*            | Tạo lệch ngang và các xoáy phụ, làm cong thêm đồ thị.                                      |

---

### 1. Lý thuyết cổ điển Hansen – Rattray (1965)

Cho chế độ *ổn định, khuấy trộn vừa phải* và coi khuếch tán thẳng đứng chi phối, nghiệm độ mặn trung bình theo chiều sâu là ([Coastal Wiki][1])

$$
\overline{S}(x)=S_0\Bigl(1-\frac{2x}{3L}\Bigr)^{\!\!3/2}, \qquad 
L\sim u_r^{-1/3},
$$

với $L$ là “độ dài xâm nhập muối” (còn phụ thuộc độ sâu, hệ số khuếch tán, v.v.). Đường cong $^{3/2}$ này *lõm xuống*: độ dốc lớn gần cửa biển và thoải dần vào trong – rõ ràng *không tuyến tính*.

---

### 2. Mô hình hàm mũ đơn giản

Nếu hình dạng kênh hội tụ gần hàm mũ và bỏ qua phân tầng, phương trình advect‑diffuse 1‑chiều cho nghiệm

$$
S(x)=S_0\,\exp(-x/L_d),
$$

thường dùng để khớp số liệu thực địa ở các cửa sông nông, hội tụ mạnh ([Coastal Wiki][2]). Hàm mũ cũng cong nhưng dốc hơn ở đầu cửa.

---

### 3. Khi nào gần đúng *tuyến tính* được?

| Trường hợp                                                    | Cơ sở thực nghiệm                                                                                                                          |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| *Cửa sông “well‑mixed”, triều mạnh, hình học gần song song* | Số liệu Delaware Estuary cho thấy “trong phần lớn chiều dài xâm nhập, $S$ giảm gần như tuyến tính với khoảng cách” ([ScienceDirect][3]). |
| *Khoảng đo hẹp*                                             | Nếu bạn chỉ quan tâm 5–10 km giữa cửa sông, hàm bậc 1 có thể sai lệch < ±1–2 PSU.                                                          |
| *Ứng dụng cần độ chính xác vừa phải*                        | Ví dụ ước tính nhanh vị trí “ranh giới nước lợ” (5–10 PSU).                                                                                |

**Lưu ý**: Tuyến tính chỉ là xấp xỉ cục bộ. Ở gần cửa biển hoặc sâu trong sông sai số tăng nhanh vì độ cong của hàm thực.


---

### 4. Thực hành đo & hiệu chuẩn

1. *Dùng cảm biến độ dẫn (EC) → Độ mặn*

   * Dải 0–35 PSU *không* tuyến tính hoàn toàn với EC; tiêu chuẩn PSS‑78 dùng đa thức bậc cao. Chỉ trong dải hẹp (≈ 10 PSU) mới gần tuyến tính.
2. *Lập transect kiểm chứng*

   * Thả CTD (Conductivity‑Temperature‑Depth) theo khoảng 1–2 km/lần đo trong một chu kỳ triều để vẽ đồ thị thực tế $S(x)$.
3. *Chọn mô hình*

   * Nếu đường cong gần đường thẳng (xác định bằng $R^2$ > 0,9) → dùng tuyến tính.
   * Ngược lại, khớp hàm mũ hoặc công thức Hansen‑Rattray rồi nội suy.

---

### 5. Gợi ý quy trình nhanh

text
1. Đo S tại cửa biển (S₀ ≈ 35 PSU) và tại đầu trên (≈ 0 PSU).
2. Khoảng cách L_est = vị trí S = 1 PSU.
3. Lấy 3–4 điểm giữa, thử hồi quy tuyến tính.
4. Nếu RMSE < 1 PSU ⇒ dùng hàm tuyến tính S(x) = a + b·x.
   Ngược lại ⇒ thử S(x)=S₀·exp(−x/L) hoặc công thức 3/2.

---

## Kết luận

* *Về bản chất*, phân bố độ mặn dọc sông‑biển *phi tuyến* do tương tác nhiều cơ chế động lực học.
* *Xấp xỉ tuyến tính*
có thể dùng khi:

  * cửa sông được trộn mạnh,
  * hình học đơn giản,
  * hoặc bạn chỉ cần độ chính xác vài PSU trên một đoạn ngắn.
* Đối với mô phỏng, quản lý cấp nước và dự báo xâm nhập mặn dài hạn, hãy sử dụng mô hình phi tuyến (hàm mũ, công thức Hansen‑Rattray hoặc mô hình số 2‑D/3‑D) để đảm bảo tin cậy.

[1]: https://www.coastalwiki.org/wiki/Estuarine_circulation "Estuarine circulation - Coastal Wiki"
[2]: https://www.coastalwiki.org/wiki/Seawater_intrusion_and_mixing_in_estuaries?utm_source=chatgpt.com "Seawater intrusion and mixing in estuaries - Coastal Wiki"
[3]: https://www.sciencedirect.com/science/article/pii/S0272771405801106?utm_source=chatgpt.com "The axial salinity distribution in the delaware estuary and its weak ..."
www.coastalwiki.org
