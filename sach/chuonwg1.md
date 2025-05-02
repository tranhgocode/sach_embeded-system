# Programming Embedded Systems in C and C++ - Chương 1: Giới thiệu

> “Tôi nghĩ rằng thị trường thế giới có thể cần khoảng năm chiếc máy tính.”  
> — Thomas Watson, Chủ tịch IBM, 1943  
>
> “Không có lý do nào để ai đó muốn có máy tính trong nhà của họ.”  
> — Ken Olson, Chủ tịch Digital Equipment Corporation, 1977

Một trong những phát triển đáng ngạc nhiên nhất của vài thập kỷ qua là vị thế ngày càng tăng của máy tính trong đời sống con người. Ngày nay có nhiều máy tính trong gia đình và văn phòng hơn cả số người sống và làm việc ở đó. Thế nhưng rất nhiều thiết bị này không được người dùng nhận ra là máy tính. Trong chương này, tôi sẽ giải thích hệ thống nhúng là gì và chúng xuất hiện ở đâu. Tôi cũng sẽ giới thiệu về lập trình nhúng, lý do tôi chọn C và C++ làm ngôn ngữ cho cuốn sách này, và phần cứng được dùng trong các ví dụ.

---

## Mục lục
1. [Hệ thống nhúng là gì?](#hệ-thống-nhúng-là-gì)
   1. [Lịch sử và tương lai](#lịch-sử-và-tương-lai)
   2. [Hệ thống thời gian thực](#hệ-thống-thời-gian-thực)
2. [Những biến thể của chủ đề](#những-biến-thể-của-chủ-đề)
   1. [Đồng hồ kỹ thuật số](#đồng-hồ-kỹ-thuật-số)
   2. [Máy chơi trò chơi điện tử](#máy-chơi-trò-chơi-điện-tử)
   3. [Thiết bị thám hiểm sao Hỏa](#thiết-bị-thám-hiểm-sao-hỏa)
3. [Ngôn ngữ C: Mẫu số chung nhỏ nhất](#ngôn-ngữ-c-mẫu-số-chung-nhỏ-nhất)
   1. [Các ngôn ngữ nhúng khác](#các-ngôn-ngữ-nhúng-khác)
   2. [Lựa chọn ngôn ngữ cho cuốn sách](#lựa-chọn-ngôn-ngữ-cho-cuốn-sách)
4. [Một vài lời về phần cứng](#một-vài-lời-về-phần-cứng)

---

## 1. Hệ thống nhúng là gì?

Hệ thống nhúng là sự kết hợp giữa phần cứng và phần mềm máy tính, và có thể còn bao gồm các thành phần cơ–điện tử hoặc các bộ phận khác, được thiết kế để thực hiện một chức năng cụ thể. Ví dụ điển hình là lò vi sóng. Hầu như mọi gia đình đều có ít nhất một chiếc, và hàng chục triệu chiếc được sử dụng mỗi ngày, nhưng rất ít người biết bên trong đó có bộ xử lý và phần mềm điều khiển.

Điều này hoàn toàn trái ngược với máy tính cá nhân (PC) trong phòng khách. Nó cũng bao gồm phần cứng máy tính, phần mềm và các thành phần cơ khí (ví dụ: ổ đĩa), nhưng không được thiết kế để làm một việc duy nhất. Thay vào đó, nó có thể đảm nhiệm nhiều tác vụ khác nhau. Người ta thường gọi nó là **máy tính đa năng**.

Thường thì, một hệ thống nhúng là một thành phần nằm trong một hệ thống lớn hơn. Ví dụ, ô‑tô và xe tải hiện đại chứa nhiều hệ thống nhúng: một hệ thống điều khiển phanh ABS, một hệ thống giám sát và kiểm soát khí thải, và một hệ thống hiển thị thông tin trên bảng điều khiển. Đôi khi các hệ thống này được kết nối qua mạng truyền thông, nhưng điều đó không phải bắt buộc.

Và, có thể gây chút nhầm lẫn, một máy tính đa năng cũng gồm nhiều hệ thống nhúng. Ví dụ, máy tính của tôi bao gồm bàn phím, chuột, card đồ họa, modem, ổ cứng, ổ đĩa mềm và card âm thanh—mỗi thiết bị đều là một hệ thống nhúng. Mỗi thiết bị chứa bộ xử lý, phần mềm và được thiết kế để thực hiện một chức năng riêng: ví dụ, modem chỉ để truyền và nhận dữ liệu số qua đường điện thoại analog.

Nếu hệ thống nhúng được thiết kế tốt, sự hiện diện của bộ xử lý và phần mềm có thể hoàn toàn không được người dùng nhận ra—như lò vi sóng, đầu VCR hay đồng hồ báo thức. Trong một số trường hợp, ta có thể thay thế bộ xử lý và phần mềm bằng một mạch tích hợp tùy biến với chức năng tương đương. Tuy nhiên, khi mã hóa cứng bằng phần cứng, ta mất rất nhiều tính linh hoạt. Thay đổi một vài dòng phần mềm rẻ và dễ dàng hơn nhiều so với thiết kế lại phần cứng tùy biến.

### 1.1 Lịch sử và tương lai

Với định nghĩa về hệ thống nhúng đã nêu, loại hệ thống này không thể xuất hiện trước năm 1971—năm Intel giới thiệu vi xử lý đầu tiên trên thế giới. Con chip 4004 được thiết kế cho dòng máy tính bỏ túi của công ty Busicom (Nhật Bản). Thay vì chế tạo mạch riêng cho từng mẫu máy, Intel đề xuất một bộ xử lý **đa năng** có thể dùng chung cho toàn bộ dòng sản phẩm, đọc và thực thi tập lệnh lưu trong bộ nhớ ngoài.

Vi xử lý đã thành công ngay tức thì, và ứng dụng của nó lan rộng trong thập niên sau đó. Những ứng dụng nhúng đầu tiên bao gồm tàu vũ trụ không người lái, đèn giao thông máy tính hóa và hệ thống điều khiển bay máy bay. Đến những năm 1980, hệ thống nhúng len lỏi vào mọi khía cạnh đời sống cá nhân và chuyên nghiệp—từ máy làm bánh mì, máy xay, lò vi sóng trong bếp, đến TV, dàn stereo, điều khiển từ xa trong phòng khách, cũng như fax, pager, máy in laser, máy tính tiền và máy quét thẻ tín dụng nơi làm việc.

Có vẻ chắc chắn rằng số lượng hệ thống nhúng sẽ tiếp tục tăng nhanh. Đã có những thiết bị nhúng tiềm năng lớn như công tắc và bộ điều nhiệt có thể điều khiển qua máy tính trung tâm, túi khí “thông minh” chỉ bung khi người ngồi là người lớn, thiết bị tổ chức cá nhân (PDA), máy ảnh kỹ thuật số và định vị trên ô‑tô.

### 1.2 Hệ thống thời gian thực

Một phân lớp quan trọng của hệ thống nhúng là **hệ thống thời gian thực**. Theo định nghĩa, đó là hệ thống máy tính có **ràng buộc thời gian**—tức các phép tính, quyết định đều phải hoàn thành trước hạn định (deadline). Việc trễ deadline nghiêm trọng không kém đưa ra kết quả sai.

Nếu hệ thống thời gian thực là một phần của hệ thống điều khiển bay máy bay, việc chậm trễ có thể gây nguy hiểm tính mạng. Nếu là hệ thống truyền thông vệ tinh, lỗi có thể chỉ làm mất gói dữ liệu. Hệ thống có hậu quả nghiêm trọng được gọi là **thời gian thực cứng** (hard real‑time), ngược lại là **mềm** (soft real‑time). Nhà thiết kế hệ thống thời gian thực phải đảm bảo phần cứng và phần mềm hoạt động đúng trong mọi tình huống.

---

## 2. Những biến thể của chủ đề

Không như phần mềm cho máy tính đa năng, phần mềm nhúng thường không thể chạy trên hệ thống nhúng khác mà không sửa đổi đáng kể, do đa dạng về phần cứng. Mỗi hệ thống được tùy biến theo ứng dụng để giảm chi phí, bỏ mạch không cần thiết và chia sẻ tài nguyên.

### 2.1 Đồng hồ kỹ thuật số

Truyền thống của đồng hồ—từ mặt trời, đồng nước, cát—được kết thúc bằng **đồng hồ số**. Các tính năng: hiển thị ngày giờ (đến giây), đo thời gian sự kiện (đến 1/100 giây), phát âm báo mỗi giờ… đều rất đơn giản, không đòi hỏi nhiều sức mạnh xử lý hay bộ nhớ. Lý do duy nhất dùng bộ xử lý là để hỗ trợ nhiều mẫu và tính năng trên cùng nền phần cứng.

Đồng hồ số điển hình dùng bộ xử lý 8‑bit rẻ tiền, thường tích hợp ROM trên chip, có khi không cần RAM nếu đủ thanh ghi. Tất cả mạch điện—bộ xử lý, bộ nhớ, bộ đếm và đồng hồ thời gian thực—đều nằm trong một chip. Phần cứng còn lại chỉ là các nút bấm (input) và LCD, loa (output).

**Mục tiêu giá thành cực thấp** khiến nhà thiết kế đôi khi hy sinh một số tính năng để giảm chi phí sản xuất: loại bỏ nút bấm, bỏ loa… mà không cần thay đổi phần mềm.

### 2.2 Máy chơi trò chơi điện tử

Khi bạn lấy Nintendo‑64 hay Sony PlayStation ra khỏi kệ, bạn đang sử dụng hệ thống nhúng. Đôi khi chúng còn mạnh hơn PC của cùng thế hệ, nhưng giá bán lại thấp hơn nhiều, khoảng 100 đô la.

Nhà sản xuất ít quan tâm đến chi phí phát triển (có thể lên đến hàng trăm nghìn đô), miễn sao chi phí sản xuất rẻ. Họ còn thiết kế bộ xử lý tùy biến với chi phí cao, nhưng cho phép bộ nhớ và các linh kiện chính dời sang **cartridge** (hộp game) thay vì bo mạch chính.

### 2.3 Thiết bị thám hiểm sao Hỏa

Năm 1976, hai tàu Viking hạ cánh lên sao Hỏa, thu thập mẫu, phân tích hóa học và truyền về Trái Đất. Giữa những chiếc PC thường xuyên phải khởi động lại, thật kinh ngạc rằng 20 năm trước, nhóm kỹ sư đã tạo ra hai máy tính sống sót sau hành trình 34 triệu dặm và hoạt động chính xác nửa thập kỷ. Rõ ràng **độ tin cậy** là yêu cầu hàng đầu.

Nếu chip nhớ hỏng, phần mềm gặp lỗi, hay kết nối điện phá vỡ khi đáp, ta không thể ngăn mọi sự cố. Vì vậy, các điểm có khả năng lỗi cao được loại trừ bằng **mạch dự phòng** hoặc chức năng bổ sung: thêm bộ xử lý, chẩn đoán bộ nhớ đặc biệt, bộ định thời phần cứng để reset khi phần mềm treo, v.v.

Gần đây, NASA triển khai Pathfinder với ngân sách tiết kiệm. Nhờ tiến bộ công nghệ, họ giảm chút độ dư thừa nhưng vẫn trang bị cho tàu: module hạ cánh dùng bộ xử lý 32‑bit, 128 MB RAM; rover dùng 8‑bit và 512 KB RAM.

---

## 3. Ngôn ngữ C: Mẫu số chung nhỏ nhất

Một trong số ít hằng số chung cho mọi hệ thống nhúng là **ngôn ngữ C**. Hơn bất kỳ ngôn ngữ nào khác, C đã trở thành ngôn ngữ của lập trình nhúng. Dù thành công nhất thường là chọn ngôn ngữ phù hợp cho dự án, thật ngạc nhiên khi một ngôn ngữ có thể dùng cho bộ xử lý 8‑bit đến 64‑bit, hệ thống có vài KB đến vài MB RAM.

C có ưu điểm nhỏ gọn, dễ học, compiler hỗ trợ hầu hết bộ xử lý, và cộng đồng lập trình viên C rất lớn. C cũng mang tính **độc lập bộ xử lý**, cho phép tập trung vào thuật toán thay vì chi tiết kiến trúc. Nhưng nhiều ưu điểm này cũng có ở ngôn ngữ cấp cao khác. Điểm mạnh nhất—và khác biệt với Pascal, FORTRAN—là C là ngôn ngữ “cấp thấp” so với hầu hết các ngôn ngữ cấp cao khác, cho phép lập trình viên nhúng tương tác trực tiếp với phần cứng.

### 3.1 Các ngôn ngữ nhúng khác

- **Assembly**: Cho phép kiểm soát triệt để phần cứng, nhưng mã khó duy trì, thiếu tính port‑able.
- **C++**: Thêm tính hướng đối tượng, namespace, template… giúp tổ chức mã lớn, nhưng đi kèm chi phí runtime phức tạp.
- **Ada**: Ngôn ngữ cho hệ thống thời gian thực, kiểm tra kiểu chặt chẽ, thích hợp cho hệ thống quân sự, hàng không, ít phổ biến ngoài lĩnh vực này.

### 3.2 Lựa chọn ngôn ngữ cho cuốn sách

Cuốn sách này ưu tiên C, C++—vừa phổ biến, vừa cân bằng được hiệu suất và tổ chức mã. Assembly chỉ được nhắc khi cần tối ưu hoặc truy cập phần cứng đặc biệt.

---

## 4. Một vài lời về phần cứng

Vì mỗi bo mạch nhúng khác nhau, việc port code là không tránh khỏi. Để minh họa, cuốn sách dùng bo mạch **Target188EB** của Arcom Control Systems, dựa trên vi xử lý Intel 80188EB (16 bit), tích hợp 128 KB RAM, 256 KB ROM và nhiều ngoại vi thông dụng.

- Nếu bạn có bo mạch tham chiếu, có thể chạy nguyên xi các ví dụ.
- Nếu không, bạn cần port code sang bo mạch mình có. Phần mã được viết cố gắng giữ tính portable, nhưng driver Flash hay ngoại vi khác có thể cần chỉnh sửa.

Trong các chương tiếp theo, chúng ta sẽ bắt đầu với ví dụ **Blinking LED**, sau đó khám phá quá trình biên dịch, liên kết và định vị mã trên hệ thống nhúng.

---

*Hết Chương 1*

