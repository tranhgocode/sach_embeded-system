# Chương 2. Chương trình nhúng đầu tiên của bạn

## Mục lục

1. [Hello, World!](#1-hello-world)
2. [Das Blinkenlights](#2-das-blinkenlights)
   1. [toggleLed](#21-toggleled)
   2. [delay](#22-delay)
3. [Vai trò của vòng lặp vô hạn](#3-vai-trò-của-vòng-lặp-vô-hạn)

---

## 1. Hello, World!

Hầu như mọi sách hướng dẫn lập trình đều bắt đầu với cùng một ví dụ — một chương trình in ra màn hình chuỗi ký tự “Hello, World!”. Ví dụ tưởng chừng sáo rỗng này lại rất hữu ích: nó cho người đọc nhanh chóng đánh giá xem việc viết những chương trình đơn giản trong môi trường mới có dễ dàng hay không. Nhưng với hệ thống nhúng, việc hiện thông điệp chuỗi ký tự lên màn hình thường phức tạp hơn nhiều hoặc thậm chí không khả thi, bởi hầu hết hệ thống nhúng không có màn hình hoặc phải có trình điều khiển màn hình (display driver) được viết trước.

Chúng ta cần một ví dụ nhỏ gọn hơn, dễ triển khai và có thể chạy trên hầu hết mọi hệ thống nhúng, với ít chỗ sai sót nhất. Trong chương này, chúng ta sẽ bắt đầu bằng chương trình nhấp nháy LED với tốc độ 1 Hz (một lần bật–tắt mỗi giây) — một ví dụ thay thế cho “Hello, World!” trong thế giới nhúng.

---

## 2. Das Blinkenlights

Mọi hệ thống nhúng chúng tôi từng gặp đều có ít nhất một LED do phần mềm điều khiển. Vì vậy, chương trình nhấp nháy LED là ví dụ lý tưởng để bắt đầu: chỉ cần vài dòng C hoặc assembly để bật/tắt LED, rất ít khả năng lỗi. Hơn nữa, hầu hết hệ thống nhúng đều có LED, nên tính di động rất cao.

Cấu trúc chính của chương trình nhấp nháy LED như sau. Phần này không phụ thuộc vào phần cứng, chỉ gọi hai hàm phụ trách việc bật/tắt LED và tạo độ trễ:

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

Trên bo Arcom, có hai LED (đỏ và xanh). Trạng thái mỗi LED do một bit trong thanh ghi P2LTCH (Port 2 I/O Latch) điều khiển. Ví dụ, bit 6 bật/tắt LED xanh. Đoạn mã minh họa sau hiện thực hàm `toggleLed`, dùng inline assembly để thao tác thanh ghi I/O:

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

Hàm này tạo độ trễ bằng cách chờ bận (busy-wait) theo số mili giây yêu cầu. Tham số `nMilliseconds` nhân với hằng `CYCLES_PER_MS` (số chu kỳ đếm) để tính tổng chu kỳ vòng lặp:

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

---

## 3. Vai trò của vòng lặp vô hạn

Một trong những khác biệt cơ bản giữa phần mềm nhúng và phần mềm trên máy tính thông thường là hầu hết chương trình nhúng kết thúc bằng một vòng lặp vô hạn. Phần mềm nhúng không bao giờ “xong việc” — nó chạy mãi cho đến khi mất điện hoặc bộ vi xử lý được khởi động lại.

Đồng thời, rất ít hệ thống nhúng chạy đa nhiệm; thường chỉ có duy nhất một chương trình. Nếu phần mềm ngừng chạy, phần cứng coi như vô dụng. Vì vậy, ta luôn bao quanh phần chức năng quan trọng bằng vòng lặp vô hạn để đảm bảo nó chạy liên tục.

> **Lưu ý:** Nếu chương trình của bạn chỉ bật tắt LED một lần rồi dừng, rất có thể bạn đã quên dùng vòng lặp vô hạn `while (1)`.

---

*Hết Chương 2.*
