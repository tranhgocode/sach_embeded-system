# Chương 2. Chương trình nhúng đầu tiên của bạn

## Mục lục

1. [Hello, World!](#1-hello-world)
2. [Das Blinkenlights](#2-das-blinkenlights)
   1. [toggleLed](#21-toggleled)
   2. [delay](#22-delay)
3. [Vai trò của vòng lặp vô hạn](#3-vai-trò-của-vòng-lặp-vô-hạn)

---

## 1. Hello, World!

Có vẻ như hầu như mọi cuốn sách hướng dẫn lập trình từ trước đến nay đều bắt đầu với cùng một ví dụ — một chương trình in ra màn hình chuỗi ký tự “Hello, World!”. Một ví dụ đã bị lạm dụng như thế có thể trông hơi nhàm chán. Nhưng nó giúp người đọc nhanh chóng đánh giá mức độ dễ dàng hay khó khăn khi viết các chương trình đơn giản trong môi trường lập trình đang dùng. Theo nghĩa đó, “Hello, World!” đóng vai trò như một tiêu chuẩn hữu ích để so sánh các ngôn ngữ lập trình và nền tảng máy tính.

Thật không may, theo thước đo này, hệ thống nhúng nằm trong số những nền tảng máy tính khó nhằn nhất để lập trình. Trên một số hệ thống nhúng, thậm chí có thể không thể hiện thực chương trình “Hello, World!”. Và trên những hệ thống có khả năng hỗ trợ nó, việc in chuỗi ký tự thường là một bước cuối cùng hơn là một khởi đầu. Bạn thấy đấy, giả thiết cơ bản của ví dụ “Hello, World!” là tồn tại một thiết bị đầu ra nào đó để in chuỗi ký tự. Một cửa sổ văn bản trên màn hình người dùng thường phục vụ mục đích đó. Nhưng hầu hết hệ thống nhúng không có màn hình hoặc thiết bị tương tự. Và những hệ thống có, thường đòi hỏi phải triển khai trước một phần mềm nhúng đặc biệt, gọi là display driver — một cách khởi đầu khá thách thức cho sự nghiệp lập trình nhúng.

Sẽ tốt hơn rất nhiều nếu bắt đầu với một chương trình nhúng nhỏ gọn, dễ triển khai và có tính di động cao, trong đó gần như không còn chỗ cho sai sót lập trình. Rốt cuộc, lý do các đồng nghiệp viết sách của tôi tiếp tục sử dụng ví dụ “Hello, World!” là vì nó quá đơn giản để triển khai. Điều này loại bỏ một biến số nếu chương trình của người đọc không chạy ngay lần đầu tiên: đó không phải là lỗi trong mã của họ; thay vào đó, có vấn đề ở công cụ phát triển hoặc quy trình họ đã dùng để tạo file thực thi.

Lập trình viên nhúng phải tự lực. Họ phải luôn bắt đầu mỗi dự án mới với giả định rằng không có gì hoạt động — tất cả những gì họ có thể dựa vào chỉ là cú pháp cơ bản của ngôn ngữ C. Ngay cả các thủ tục thư viện chuẩn cũng có thể không có sẵn đối với họ. Đó là những hàm phụ trợ — như printf và scanf — mà hầu hết lập trình viên khác xem là điều hiển nhiên. Thực ra, thủ tục thư viện thường là một phần của chuẩn ngôn ngữ ngang hàng với cú pháp cơ bản. Tuy nhiên, phần chuẩn này khó hỗ trợ trên mọi nền tảng máy tính và đôi khi bị những nhà sản xuất trình biên dịch cho hệ thống nhúng lược bỏ.

Vì vậy, bạn sẽ không tìm thấy một chương trình “Hello, World!” thật sự trong chương này. Thay vào đó, chúng ta sẽ chỉ giả định cú pháp cơ bản của C có sẵn cho ví dụ đầu tiên. Khi tiến tới các chương sau, chúng ta sẽ dần thêm cú pháp C++, thủ tục thư viện chuẩn và tương đương của thiết bị xuất ký tự vào ngăn xếp của mình. Rồi đến chương 9, chúng ta sẽ triển khai chương trình “Hello, World!”. Khi đó, bạn sẽ đã trên con đường trở thành chuyên gia trong lĩnh vực lập trình hệ thống nhúng.

---

## 2. Das Blinkenlights

Mọi hệ thống nhúng chúng tôi từng gặp đều có ít nhất một LED do phần mềm điều khiển. Vì vậy, thay thế cho chương trình “Hello, World!” của tôi là chương trình nhấp nháy LED với tốc độ 1 Hz (một chu kỳ bật–tắt đầy đủ mỗi giây). Thông thường, mã để bật và tắt LED chỉ gói gọn trong vài dòng C hoặc assembly, nên rất ít khả năng xảy ra lỗi lập trình. Và vì hầu hết các hệ thống nhúng đều có LED, nên khái niệm cơ bản này có tính di động rất cao.

[1] Tất nhiên, tần số nhấp nháy hoàn toàn tùy ý. Nhưng một trong những điểm tôi thích ở tần số 1 Hz là dễ xác nhận bằng đồng hồ bấm giây. Đơn giản là bắt đầu đồng hồ, đếm số lần nhấp nháy, rồi xem số giây trôi qua có bằng số lần nhấp nháy hay không. Cần độ chính xác cao hơn? Chỉ cần đếm thêm nhiều lần nhấp nháy hơn.

Siêu cấu trúc của chương trình LED nhấp nháy được thể hiện dưới đây. Phần này không phụ thuộc vào phần cứng. Tuy nhiên, nó dựa vào hai hàm phụ thuộc phần cứng toggleLed và delay để thay đổi trạng thái LED và xử lý thời gian, tương ứng.

```c
/**********************************************************************
 *
 * Hàm:       main()
 *
 * Mô tả:     Nhấp nháy LED màu xanh lá một lần mỗi giây.
 *
 * Ghi chú:   Vòng lặp ngoài không phụ thuộc phần cứng. Tuy nhiên,
 *            nó dựa vào hai hàm phụ thuộc phần cứng.
 *
 * Trả về:    Hàm này chứa vòng lặp vô hạn, không bao giờ kết thúc.
 *
 **********************************************************************/
void 
main(void)
{
    while (1)
    {
        toggleLed(LED_GREEN);      /* Thay đổi trạng thái của LED.    */
        delay(500);                /* Tạm dừng 500 milli giây.        */
    }
}   /* main() */
```

### 2.1. toggleLed

Trên bo Arcom, thực tế có hai LED: một đỏ và một xanh lá. Trạng thái của mỗi LED được điều khiển bởi một bit trong thanh ghi Port 2 I/O Latch Register (P2LTCH). Thanh ghi này nằm trong chính chip CPU và được đặt tên như vậy vì nó chứa trạng thái latch của tám chân I/O bên ngoài chip, được gọi chung là I/O Port 2. Mỗi trong tám bit của thanh ghi P2LTCH tương ứng với điện áp trên một trong các chân I/O đó. Ví dụ, bit 6 điều khiển điện áp cấp cho LED màu xanh lá:

#define <mark>LED_GREEN</mark> 0x40 /* LED xanh lá được điều khiển bởi bit 6 */

Bằng cách sửa đổi bit này, ta có thể thay đổi điện áp trên chân ngoài và từ đó thay đổi trạng thái của LED. Như minh họa trong Hình 2-1, khi bit 6 của thanh ghi P2LTCH là 1, LED tắt; khi nó là 0, LED sáng.

Thanh ghi P2LTCH nằm ở vùng nhớ đặc biệt gọi là I/O space, tại offset 0xFF5E. Thật không may, các thanh ghi trong I/O space của bộ xử lý 80x86 chỉ có thể được truy cập thông qua các lệnh assembly in và out. Ngôn ngữ C không hỗ trợ trực tiếp các hoạt động này. Thay thế gần nhất là các hàm thư viện inport và outport khai báo trong tập tin đầu vào dos.h chuyên cho PC. Lý tưởng nhất, chúng ta sẽ chỉ cần bao gồm tập tin đó và gọi trực tiếp các hàm trên trong chương trình nhúng. Tuy nhiên, vì chúng thuộc thư viện lập trình DOS, ta phải giả định trường hợp xấu nhất: chúng có thể không hoạt động trên hệ thống của chúng ta. Ít nhất, chúng ta không nên phụ thuộc vào chúng trong chương trình đầu tiên này.

Đoạn cài đặt hàm toggleLed dành riêng cho bo Arcom và không phụ thuộc hàm thư viện nào được minh họa dưới đây. Thuật toán rất đơn giản: đọc giá trị hiện tại của thanh ghi P2LTCH, đảo bit điều khiển LED mong muốn, và ghi giá trị mới trở lại thanh ghi. Bạn sẽ nhận thấy mặc dù hàm này được viết bằng C, phần chức năng thực sự lại được hiện thực bằng assembly. Đây là một kỹ thuật hữu ích, gọi là inline assembly, tách biệt lập trình viên khỏi các chi tiết về convention gọi hàm và truyền tham số của C, đồng thời vẫn tận dụng được đầy đủ sức mạnh của ngôn ngữ assembly.

```c
#define P2LTCH      0xFF5E      /* Địa chỉ thanh ghi P2LTCH. */

/**********************************************************************
 *
 * Hàm:       toggleLed()
 *
 * Mô tả:     Đảo trạng thái một hoặc cả hai LED.
 *
 * Ghi chú:   Chỉ dành cho bo Arcom Target188EB.
 *
 **********************************************************************/
void  
toggleLed(unsigned char ledMask)
{
    asm {
        mov dx, P2LTCH          /* Tải địa chỉ thanh ghi.          */
        in  al, dx              /* Đọc nội dung thanh ghi.         */

        mov ah, ledMask         /* Đưa ledMask vào thanh ghi.      */
        xor al, ah              /* Đảo bit LED tương ứng.          */

        out dx, al              /* Ghi ngược lại vào thanh ghi.     */
    };
}   /* toggleLed() */
```

### 2.2 delay

Chúng ta cần thêm khoảng dừng nửa giây (500 ms) giữa các lần đổi trạng thái LED. Khoảng dừng này được thực hiện bằng cách bận chờ (busy-wait) trong hàm delayMs dưới đây. Hàm này nhận độ dài thời gian trễ (tính theo mili giây) làm tham số duy nhất, rồi nhân giá trị đó với hằng số CYCLES_PER_MS để tính tổng số lần lặp của vòng while cần thiết cho khoảng thời gian trễ yêu cầu.

```c
/**********************************************************************
 *
 * Hàm:       delay()
 *
 * Mô tả:     Chờ bận trong số mili giây cho trước.
 *
 * Ghi chú:   Giá trị CYCLES_PER_MS xác định số chu kỳ đếm, phụ
 *            thuộc tốc độ và loại CPU.
 *
 **********************************************************************/
void  
delay(unsigned int nMilliseconds)
{
    #define CYCLES_PER_MS 260 /* Số chu kỳ đếm mỗi ms. */

    unsigned long nCycles = nMilliseconds * CYCLES_PER_MS;

    while (nCycles--);
}   /* delay() */
```

Hằng số đặc thù phần cứng CYCLES_PER_MS đại diện cho số vòng lặp giảm và kiểm tra (nCycles-- != 0) mà bộ xử lý có thể thực hiện trong một mili giây. Để xác định con số này, tôi đã sử dụng phương pháp thử và sai. Tôi đã tính toán sơ bộ (tôi nghĩ nó ra khoảng 200), rồi viết nốt phần còn lại của chương trình, biên dịch và chạy thử. Thực tế, LED đã nhấp nháy nhưng với tần số nhanh hơn 1 Hz. Vì vậy, tôi đã dùng đồng hồ bấm giờ đáng tin cậy để thực hiện một loạt thay đổi nhỏ lên CYCLES_PER_MS cho đến khi tốc độ nhấp nháy gần 1 Hz nhất có thể theo mức thử nghiệm của tôi.

Chừng đó thôi! Đó là toàn bộ chương trình Blinking LED. Ba hàm main, toggleLed và delay đã thực hiện trọn vẹn mọi công việc. Nếu bạn muốn chuyển chương trình này sang hệ thống nhúng khác, bạn nên đọc tài liệu kèm theo phần cứng của mình, viết lại hàm toggleLed cho phù hợp và thay đổi giá trị của CYCLES_PER_MS. Tất nhiên, chúng ta vẫn cần bàn về cách xây dựng và chạy chương trình này. Chúng ta sẽ xem xét các chủ đề đó trong hai chương tiếp theo. Nhưng trước hết, tôi có vài lời muốn nói về vòng lặp vô hạn và vai trò của chúng trong hệ thống nhúng.

---

## 3. Vai trò của vòng lặp vô hạn

Một trong những khác biệt cơ bản nhất giữa các chương trình phát triển cho hệ thống nhúng và những chương trình viết cho các nền tảng máy tính khác là các chương trình nhúng hầu như luôn kết thúc bằng một vòng lặp vô hạn. Thường thì vòng lặp này bao quanh phần lớn chức năng của chương trình—như trong chương trình Blinking LED. Vòng lặp vô hạn này là cần thiết vì công việc của phần mềm nhúng không bao giờ kết thúc. Nó được thiết kế để chạy cho đến khi thế giới này chấm dứt hoặc bo mạch được đặt lại, tùy sự kiện nào xảy ra trước.

Ngoài ra, hầu hết các hệ thống nhúng chỉ có một phần mềm duy nhất chạy trên đó. Và mặc dù phần cứng quan trọng, nó không phải là một chiếc đồng hồ kỹ thuật số hay một chiếc điện thoại di động hay một lò vi sóng nếu thiếu phần mềm nhúng đó. Nếu phần mềm ngừng chạy, phần cứng trở nên vô dụng. Vì vậy, các phần chức năng của chương trình nhúng hầu như luôn được bao quanh bởi một vòng lặp vô hạn nhằm đảm bảo chúng sẽ chạy mãi mãi.

Hành vi này phổ biến đến mức gần như không đáng nhắc đến. Và tôi cũng sẽ không nhắc, nếu không phải vì tôi đã thấy khá nhiều lập trình viên nhúng lần đầu bị nhầm lẫn bởi sự khác biệt tinh tế này. Vì vậy, nếu chương trình đầu tiên của bạn có vẻ như chạy, nhưng thay vì nhấp nháy LED nó chỉ thay đổi trạng thái một lần, rất có thể bạn đã quên bao quanh các lời gọi đến toggleLed và delay bằng một vòng lặp vô hạn.

> **Lưu ý:** Nếu chương trình của bạn chỉ bật tắt LED một lần rồi dừng, rất có thể bạn đã quên dùng vòng lặp vô hạn `while (1)`.

---

*Hết Chương 2.*
