# Programming Embedded Systems in C and C++ - Chương 1: Giới thiệu

> “Tôi nghĩ rằng thị trường thế giới có thể cần khoảng năm chiếc máy tính.”  
> — Thomas Watson, Chủ tịch IBM, 1943  
>
> “Không có lý do nào để ai đó muốn có máy tính trong nhà của họ.”  
> — Ken Olson, Chủ tịch Digital Equipment Corporation, 1977

Một trong những phát triển đáng ngạc nhiên nhất của vài thập kỷ qua là vị thế ngày càng tăng của máy tính trong đời sống con người. Ngày nay có nhiều máy tính trong gia đình và văn phòng hơn cả số người sống và làm việc ở đó. Thế nhưng rất nhiều thiết bị này không được người dùng nhận ra là máy tính. Trong chương này, tôi sẽ giải thích hệ thống nhúng là gì và chúng xuất hiện ở đâu. Tôi cũng sẽ giới thiệu về lập trình nhúng, lý do tôi chọn C và C++ làm ngôn ngữ cho cuốn sách này, và phần cứng được dùng trong các ví dụ.

---

## Mục lục
1. [Hệ thống nhúng là gì?](#1-hệ-thống-nhúng-là-gì)
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

Không như ***phần mềm*** được thiết kế cho máy tính đa năng, ***phần mềm*** nhúng thường không thể chạy trên các hệ thống nhúng khác mà không có sự sửa đổi đáng kể. Điều này chủ yếu bởi sự đa dạng khổng lồ của phần cứng nền tảng. Phần cứng trong mỗi hệ thống nhúng được thiết kế riêng cho ứng dụng nhằm giữ chi phí tổng thể ở mức thấp nhất. Do đó, các mạch không cần thiết được loại bỏ và tài nguyên phần cứng được chia sẻ bất cứ khi nào có thể.

Trong phần này, bạn sẽ tìm hiểu những tính năng phần cứng chung trên mọi hệ thống nhúng và lý do tại sao hầu hết mọi thứ khác lại có rất nhiều biến thể.

Theo định nghĩa, tất cả hệ thống nhúng đều chứa ***bộ xử lý*** và ***phần mềm***, nhưng còn những đặc điểm chung nào khác? Chắc chắn, để có ***phần mềm*** thì phải có nơi lưu trữ mã thực thi và nơi lưu trữ tạm thời để xử lý dữ liệu trong lúc chạy. Chúng tồn tại dưới dạng ***ROM*** và ***RAM*** tương ứng; bất kỳ hệ thống nhúng nào cũng sẽ có ít nhất một loại mỗi loại. Nếu chỉ cần một lượng nhỏ bộ nhớ, nó có thể được tích hợp ngay trong cùng chip với ***bộ xử lý***. Ngược lại, một hoặc cả hai loại bộ nhớ thường được đặt trên các chip ngoại vi.

Tất cả hệ thống nhúng cũng đều có các ***ngõ vào*** và ***ngõ ra*** nhất định. Ví dụ, trong lò vi sóng, ***ngõ vào*** là các nút bấm trên bảng điều khiển và cảm biến nhiệt độ; ***ngõ ra*** là màn hình hiển thị cho người dùng và bức xạ vi sóng. Hầu như luôn đúng rằng ***ngõ ra*** của hệ thống nhúng là một hàm số của ***ngõ vào*** cùng với một số yếu tố khác (thời gian trôi qua, nhiệt độ hiện tại, v.v.). Ngõ vào thường ở dạng cảm biến, tín hiệu liên lạc hoặc núm bấm điều khiển; ***ngõ ra*** thường là màn hình, tín hiệu liên lạc hoặc các tác động vật lý tới thế giới bên ngoài.

Ngoài những đặc điểm chung nêu trên, phần còn lại của phần cứng nhúng thường rất riêng biệt. Sự đa dạng này xuất phát từ nhiều tiêu chí thiết kế khác nhau. Mỗi hệ thống phải đáp ứng một tập hợp yêu cầu hoàn toàn riêng biệt, mà bất kỳ yêu cầu nào trong đó cũng có thể ảnh hưởng đến những thỏa hiệp và đánh đổi khi phát triển sản phẩm. Chẳng hạn, nếu hệ thống phải có chi phí sản xuất dưới 10 USD, thì các yếu tố khác như công suất xử lý và độ tin cậy của hệ thống có thể phải hy sinh để đáp ứng mục tiêu đó.

Tất nhiên, chi phí sản xuất chỉ là một trong những ràng buộc mà các kỹ sư phần cứng nhúng phải cân nhắc. Các yêu cầu thiết kế khác thường gặp bao gồm:

- ***Công suất xử lý (Processing power):*** Lượng công suất cần thiết để hoàn thành công việc. Một chỉ số thường dùng để so sánh là MIPS (triệu chỉ thị mỗi giây). Ví dụ, ***bộ xử lý*** 40 MIPS được coi mạnh hơn 25 MIPS. Tuy nhiên, còn nhiều đặc điểm quan trọng khác của ***bộ xử lý*** cần xét đến, như độ rộng thanh ghi (từ 8 đến 64 bit). Máy tính đa năng hiện thường dùng vi xử lý 32 và 64 bit, nhưng nhiều hệ thống nhúng vẫn sử dụng vi xử lý 8 và 16 bit cũ hơn vì chi phí thấp hơn.

- ***Bộ nhớ (Memory):*** Lượng bộ nhớ (***ROM*** và ***RAM***) cần thiết để chứa ***phần mềm*** và dữ liệu trong lúc chạy. Kỹ sư phần cứng thường phải ước tính trước và điều chỉnh lượng bộ nhớ thực tế trong quá trình phát triển ***phần mềm***. Lượng bộ nhớ cần dùng cũng ảnh hưởng đến việc chọn vi xử lý, bởi độ rộng thanh ghi địa chỉ xác định giới hạn tối đa vùng nhớ có thể truy cập (ví dụ, thanh ghi địa chỉ 8 bit chỉ chọn được 256 ô nhớ).[1]

  [1] Tất nhiên, thanh ghi địa chỉ càng nhỏ, ***bộ xử lý*** càng có xu hướng dùng các thủ thuật như không gian địa chỉ phân trang để hỗ trợ thêm bộ nhớ. Một vài trăm byte thì không làm được gì nhiều; vài nghìn byte thường là mức tối thiểu hợp lý, ngay cả với vi xử lý 8 bit.

- ***Chi phí phát triển (Development cost):*** Chi phí thiết kế phần cứng và ***phần mềm*** ban đầu. Đây là chi phí cố định, một lần, nên đôi khi không phải vấn đề (với sản phẩm sản xuất số lượng lớn), hoặc có thể là thước đo chính xác nhất của chi phí hệ thống (với số lượng ít).

- ***Số lượng sản xuất (Number of units):*** Đánh đổi giữa chi phí phát triển và chi phí sản xuất phụ thuộc lớn vào số lượng đơn vị dự kiến sản xuất và bán. Ví dụ, thường không kinh tế để phát triển linh kiện phần cứng tùy biến cho sản phẩm sản xuất quy mô nhỏ.

- ***Thời gian hoạt động dự kiến (Expected lifetime):*** Hệ thống cần hoạt động được trong bao lâu (trung bình)? Một tháng, một năm hay một thập kỷ? Điều này ảnh hưởng nhiều quyết định thiết kế, từ lựa chọn linh kiện đến chi phí phát triển và sản xuất.

- ***Độ tin cậy (Reliability):*** Mức độ tin cậy mong muốn của sản phẩm. Nếu chỉ là đồ chơi trẻ em, có thể chấp nhận lỗi đôi lần; nhưng nếu là bộ phận trong tên lửa hay ô tô, thì phải đảm bảo hoạt động chính xác mọi lần.

Bên cạnh các yêu cầu chung trên, vẫn còn những yêu cầu chức năng chi tiết tạo nên đặc thù của hệ thống nhúng—cho dù đó là lò vi sóng, máy tạo nhịp tim hay máy nhắn tin.

Bảng 1-1 minh họa phạm vi giá trị có thể cho mỗi yêu cầu thiết kế kể trên. Đây chỉ là các con số ước tính và không nên hiểu quá nghiêm túc; trong nhiều trường hợp, các tiêu chí liên quan chặt chẽ với nhau. Ví dụ, tăng công suất xử lý có thể làm tăng chi phí sản xuất, nhưng cũng có thể giảm chi phí phát triển nhờ giảm độ phức tạp trong thiết kế phần cứng và ***phần mềm***. Do đó, các giá trị trong cùng một cột không nhất thiết phải đi đôi với nhau.

<div align="center">
Bảng 1-1. Yêu cầu thiết kế chung cho hệ thống nhúng

| Tiêu chí                           | Thấp                   | Trung bình             | Cao                         |
|------------------------------------|------------------------|------------------------|-----------------------------|
| **Bộ xử lý**                       | 4- hoặc 8-bit          | 16-bit                 | 32- hoặc 64-bit            |
| **Bộ nhớ**                         | < 16 KB                | 64 KB – 1 MB           | > 1 MB                      |
| **Chi phí phát triển**             | < 100.000 USD          | 100.000 – 1.000.000 USD| > 1.000.000 USD             |
| **Chi phí sản xuất**               | < 10 USD               | 10 – 1.000 USD         | > 1.000 USD                 |
| **Số lượng sản xuất**              | < 100                  | 100 – 10.000           | > 10.000                    |
| **Thời gian hoạt động dự kiến**    | vài ngày – vài tháng   | vài năm               | vài thập kỷ                 |
| **Độ tin cậy**                     | đôi khi có thể lỗi     | phải hoạt động ổn định| tuyệt đối không lỗi         |
</div>

Để đồng thời **_minh họa_** sự **_đa dạng_** từ hệ thống nhúng này sang hệ thống nhúng khác và những **_ảnh hưởng_** có thể của các **_yêu cầu thiết kế_** lên phần cứng, tôi sẽ dành ít phút mô tả chi tiết ba hệ thống nhúng. Mục tiêu của tôi là giúp bạn **_đặt mình_** vào vị trí **_nhà thiết kế hệ thống_** trong giây lát, trước khi chúng ta bắt đầu thu hẹp phạm vi thảo luận sang **_phát triển phần mềm nhúng_**

### 2.1 Đồng hồ kỹ thuật số

Ở cuối con đường phát triển bắt đầu bằng ***đồng hồ mặt trời***, ***đồng hồ nước*** và ***đồng hồ cát*** là ***đồng hồ kỹ thuật số***. Trong số nhiều tính năng của nó có: hiển thị **ngày và giờ** (thường đến giây gần nhất), đo độ dài sự kiện đến phần trăm giây (1/100 giây), và phát ra âm thanh nhỏ gây khó chịu vào đầu mỗi giờ. Thực tế, đó là những tác vụ rất đơn giản, không đòi hỏi nhiều sức mạnh xử lý hay bộ nhớ. Thật vậy, lý do duy nhất để sử dụng ***bộ xử lý*** là để hỗ trợ nhiều mẫu mã và tính năng khác nhau từ một thiết kế phần cứng duy nhất.

***Đồng hồ kỹ thuật số*** điển hình chứa ***bộ xử lý*** ***8-bit*** đơn giản và giá rẻ. Bởi vì những bộ xử lý nhỏ này không thể **địa chỉ** nhiều bộ nhớ, loại ***bộ xử lý*** này thường tích hợp ***ROM*** trên chip. Và nếu có đủ thanh ghi, ứng dụng này có thể không cần bất kỳ ***RAM*** nào cả. Thực tế, toàn bộ mạch điện - ***bộ xử lý***, **bộ nhớ**, bộ đếm và **đồng hồ thời gian thực** - có thể được chứa trong một chip duy nhất. Các thành phần phần cứng khác của đồng hồ chỉ là ***ngõ vào*** (các nút bấm) và ***ngõ ra*** (màn hình LCD và loa).

Mục tiêu của nhà thiết kế đồng hồ là tạo ra một sản phẩm có độ tin cậy tương đối cao với chi phí sản xuất vô cùng thấp. Nếu sau sản xuất, một số mẫu chạy chính xác hơn phần lớn, chúng có thể được bán với thương hiệu cao cấp hơn để tăng lợi nhuận. Ngược lại, vẫn có thể có lợi nhuận khi bán qua kênh giảm giá. Đối với các phiên bản giá rẻ hơn, có thể loại bỏ nút bấm của đồng hồ bấm giờ hoặc loa. Điều này sẽ giới hạn chức năng của đồng hồ, nhưng có thể không cần thay đổi bất kỳ ***phần mềm*** nào. Và đương nhiên, chi phí phát triển của tất cả nỗ lực này có thể khá cao, vì nó sẽ được khấu hao trên hàng trăm nghìn hoặc hàng triệu sản phẩm bán ra.

### 2.2 Máy chơi trò chơi điện tử

Khi bạn rút ***Nintendo-64*** hoặc ***Sony PlayStation*** ra khỏi tủ giải trí, bạn đang chuẩn bị sử dụng một ***hệ thống nhúng***. Trong một số trường hợp, những máy này thậm chí còn mạnh hơn thế hệ máy tính cá nhân tương đương. Tuy nhiên, máy chơi ***game*** tại gia vẫn tương đối rẻ so với máy tính cá nhân. Chính sự đối lập giữa yêu cầu về ***công suất xử lý*** cao và ***chi phí sản xuất*** thấp đã khiến các nhà thiết kế máy chơi ***game*** phải trăn trở (và con cái họ thì được chăm bẵm đầy đủ).

Các công ty sản xuất máy chơi ***game*** thường không quá quan tâm đến ***chi phí phát triển***, miễn là ***chi phí sản xuất*** của sản phẩm cuối cùng đủ thấp—thường vào khoảng một trăm đô-la Mỹ. Họ thậm chí khuyến khích kỹ sư thiết kế ***bộ xử lý*** tùy biến với chi phí phát triển lên đến hàng trăm nghìn đô-la mỗi con. Vì vậy, dù bên trong máy có thể là ***bộ xử lý*** 64-bit, nhưng không nhất thiết giống loại ***bộ xử lý*** được dùng trong máy tính cá nhân 64-bit. Thay vào đó, ***bộ xử lý*** này thường được thiết kế chuyên biệt để đáp ứng yêu cầu của các trò chơi điện tử.

Bởi ***chi phí sản xuất*** vô cùng quan trọng trên thị trường máy chơi ***game*** gia đình, các nhà thiết kế còn áp dụng nhiều thủ thuật để tái phân bổ chi phí. Ví dụ, một chiến thuật phổ biến là dời càng nhiều ***bộ nhớ*** và linh kiện ngoại vi càng tốt ra khỏi bo mạch chính và lên các ***cartridge trò chơi***. Cách làm này giảm chi phí bo mạch chính nhưng làm tăng giá bán mỗi ***trò chơi***. Do đó, mặc dù hệ thống có thể sở hữu ***bộ xử lý*** 64-bit mạnh mẽ, bo mạch chính chỉ còn vài megabyte ***bộ nhớ*** vừa đủ để khởi động, rồi truy cập ***bộ nhớ*** bổ sung trên ***cartridge trò chơi***.


### 2.3 Thiết bị thám hiểm sao Hỏa

Năm 1976, hai tàu vũ trụ không người lái **Viking** hạ cánh lên sao Hỏa, thu thập mẫu đất, phân tích thành phần hóa học và truyền kết quả về Trái Đất. Giữa lúc máy tính cá nhân còn thường xuyên phải khởi động lại, thật đáng kinh ngạc khi hơn hai mươi năm trước, nhóm nhà khoa học–kỹ sư đã tạo ra hai **máy tính** sống sót sau hành trình 34 triệu dặm và hoạt động chính xác gần nửa thập kỷ. Rõ ràng, **_độ tin cậy_** là một trong những yêu cầu quan trọng nhất đối với các hệ thống này. Nếu **_chip nhớ_** hỏng? Hay **_phần mềm_** gặp lỗi làm treo? Hoặc kết nối điện bị đứt khi va chạm? Không có cách nào ngăn ngừa hoàn toàn các sự cố này. Vì vậy, mọi điểm có thể hỏng đều phải được loại bỏ hoặc giảm thiểu thông qua việc thêm **mạch dự phòng** và chức năng bổ sung: thêm **bộ xử lý** dự phòng, chẩn đoán bộ nhớ đặc biệt, bộ định thời phần cứng để reset khi **phần mềm** treo, v.v.

Gần đây, NASA triển khai sứ mệnh **Pathfinder** với mục tiêu chứng minh khả năng tiếp cận sao Hỏa trong ngân sách tiết kiệm. Nhờ tiến bộ công nghệ, họ giảm độ dư thừa một chút, nhưng vẫn trang bị cho Pathfinder nhiều **_công suất xử lý_** và **_bộ nhớ_** hơn Viking từng có. **Mars Pathfinder** thực chất gồm hai hệ thống nhúng: **phương tiện hạ cánh** và **rover**. Phương tiện hạ cánh dùng **bộ xử lý** 32‑bit, 128 MB **RAM**; rover dùng **bộ xử lý** 8‑bit, 512 KB **RAM**. Các lựa chọn này phản ánh yêu cầu chức năng khác nhau của hai hệ thống. Và chắc chắn, **_chi phí sản xuất_** không phải là vấn đề với NASA.

---

## 3. Ngôn ngữ C: Mẫu số chung nhỏ nhất

Một trong số ít hằng số chung cho mọi hệ thống này là việc sử dụng ngôn ngữ lập trình <mark>C</mark>. Hơn bất kỳ ngôn ngữ nào khác, C đã trở thành ngôn ngữ của các lập trình viên nhúng. Điều này không luôn đúng trong quá khứ và sẽ không kéo dài mãi mãi, nhưng hiện tại, C là tiêu chuẩn gần nhất trong thế giới nhúng. Trong phần này, tôi sẽ giải thích tại sao C trở nên phổ biến và lý do tôi chọn nó cùng hậu duệ C++ làm ngôn ngữ chính của cuốn sách này.

Vì thành công trong phát triển phần mềm thường phụ thuộc vào việc chọn ngôn ngữ tốt nhất cho dự án, thật ngạc nhiên khi một ngôn ngữ duy nhất phù hợp cho cả <mark>vi xử lý</mark> 8-bit và 64-bit; trong các hệ thống có vài byte, kilobyte và megabyte bộ nhớ; và cho các đội phát triển từ một đến hơn chục người. Tuy nhiên, đó chính là phạm vi dự án mà C đã tỏa sáng.

Tất nhiên, C có nhiều ưu điểm. Nó nhỏ gọn và khá dễ học, compiler có sẵn cho hầu hết các vi xử lý hiện nay, và cộng đồng lập trình viên C rất lớn. Thêm vào đó, C có lợi thế về <mark>độc lập bộ xử lý</mark>, cho phép lập trình viên tập trung vào thuật toán và ứng dụng thay vì chi tiết kiến trúc vi xử lý. Tuy vậy, nhiều ưu điểm này cũng có ở các ngôn ngữ cấp cao khác. Vậy tại sao C thành công còn nhiều ngôn ngữ khác thì không?

Có lẽ sức mạnh lớn nhất của C—và điểm phân biệt với Pascal hay FORTRAN—là nó là ngôn ngữ <mark>“cấp thấp”</mark> trong số các ngôn ngữ cấp cao. Như chúng ta sẽ thấy khắp cuốn sách, C cho phép lập trình viên nhúng điều khiển phần cứng một cách trực tiếp đáng kinh ngạc mà không hy sinh lợi ích của ngôn ngữ cấp cao. Tính <mark>“cấp thấp”</mark> của C là ý đồ rõ ràng của người tạo ra ngôn ngữ. Thật vậy, Kernighan và Ritchie đã viết trong trang mở đầu cuốn *The C Programming Language*:

> C is a relatively “low level” language. This characterization is not pejorative; it simply means that C deals with the same sort of objects that most computers do. These may be combined and moved about with the arithmetic and logical operators implemented by real machines.

> Few popular high-level languages can compete with C in the production of compact, efficient code for almost all processors. And, of these, only C allows programmers to interact with the underlying hardware so easily.


### 3.1 Các ngôn ngữ nhúng khác

- **Assembly**: Cho phép kiểm soát triệt để phần cứng, nhưng mã khó duy trì, thiếu tính port‑able.
- **C++**: Thêm tính hướng đối tượng, namespace, template… giúp tổ chức mã lớn, nhưng đi kèm chi phí runtime phức tạp.
- **Ada**: Ngôn ngữ cho hệ thống thời gian thực, kiểm tra kiểu chặt chẽ, thích hợp cho hệ thống quân sự, hàng không, ít phổ biến ngoài lĩnh vực này.


Tất nhiên, <mark>Assembly</mark> không phải là ngôn ngữ duy nhất mà lập trình viên nhúng sử dụng. Ít nhất còn ba ngôn ngữ khác đáng nhắc đến:

- **<mark>Assembly</mark>**: Trong những ngày đầu, phần mềm nhúng được viết hoàn toàn bằng <mark>Assembly</mark> của bộ xử lý mục tiêu. Điều này cho phép lập trình viên kiểm soát hoàn toàn ***phần cứng***, nhưng đổi lại là **chi phí phát triển cao** và **thiếu tính di động (portability)** của mã nguồn. Ngày nay, việc tìm lập trình viên có kinh nghiệm <mark>Assembly</mark> cũng ngày càng khó. Ngôn ngữ <mark>Assembly</mark> chỉ còn được dùng phụ trợ cho ngôn ngữ cấp cao, thường là cho những đoạn mã phải đạt hiệu năng hoặc kích thước cực kỳ tối ưu.

- **<mark>C++</mark>**: Là superset hướng đối tượng của C, <mark>C++</mark> ngày càng được ưa chuộng trong lập trình nhúng. Tất cả tính năng cơ bản giống C, nhưng <mark>C++</mark> bổ sung khả năng **trừu tượng dữ liệu** và phong cách **lập trình hướng đối tượng**. Những tính năng này giúp tổ chức mã tốt hơn nhưng đôi khi làm giảm **hiệu năng** chương trình. Do đó, <mark>C++</mark> thường phổ biến với các đội phát triển lớn, nơi lợi ích cho lập trình viên vượt trội hơn mức mất về hiệu năng.

- **<mark>Ada</mark>**: Cũng là ngôn ngữ hướng đối tượng, <mark>Ada</mark> khác biệt nhiều so với <mark>C++</mark>. <mark>Ada</mark> được Bộ Quốc phòng Mỹ thiết kế cho phần mềm quân sự quan trọng. Mặc dù đã là tiêu chuẩn quốc tế (Ada83 và Ada95), <mark>Ada</mark> vẫn chưa phổ biến rộng rãi ngoài ngành quốc phòng và hàng không, và đang dần mất ưu thế. Đây thật tiếc vì <mark>Ada</mark> có nhiều tính năng có thể **đơn giản hóa phát triển nhúng** nếu được sử dụng thay <mark>C++</mark>.


### 3.2 Lựa chọn ngôn ngữ cho cuốn sách

Vấn đề lớn mà tác giả cuốn sách này phải đối mặt là nên đưa những <mark>ngôn ngữ lập trình</mark> nào vào phần <mark>thảo luận</mark>? Việc <mark>bao quát</mark> quá nhiều ngôn ngữ có thể làm <mark>bối rối độc giả</mark> hoặc <mark>làm xao nhãng</mark> những điểm quan trọng hơn. Ngược lại, tập trung quá hẹp có thể khiến thảo luận trở nên quá <mark>hàn lâm</mark> hoặc (tệ hơn với tác giả và nhà xuất bản) hạn chế <mark>thị trường tiềm năng</mark> của cuốn sách.

Dĩ nhiên, <mark>C</mark> phải là <mark>trọng tâm</mark> của bất kỳ cuốn sách nào về lập trình nhúng—và cuốn sách này không ngoại lệ. Hơn một nửa mã mẫu được viết bằng C, và thảo luận sẽ chủ yếu xoay quanh các vấn đề liên quan đến C. Tất nhiên, mọi điều nói về lập trình C đều áp dụng tương tự cho C++. Thêm vào đó, tôi sẽ giới thiệu các tính năng của C++ hữu ích nhất cho phát triển phần mềm nhúng và áp dụng chúng trong các ví dụ sau. Ngôn ngữ <mark>assembly</mark> sẽ được thảo luận trong những ngữ cảnh hạn chế nhất, nhưng sẽ được tránh khi có thể. Nói cách khác, tôi chỉ đề cập assembly khi một tác vụ lập trình cụ thể không thể thực hiện theo cách khác.

Tôi cho rằng cách xử lý <mark>hỗn hợp</mark> C, C++ và assembly này phản ánh chính xác cách phát triển phần mềm nhúng hiện nay và trong tương lai gần. Tôi hy vọng lựa chọn này sẽ giữ cho cuộc thảo luận <mark>rõ ràng</mark>, cung cấp thông tin hữu ích cho người phát triển hệ thống thực tế, và thu hút được <mark>độc giả</mark> rộng nhất có thể.


---

## 4. Một vài lời về phần cứng

Trong lập trình, sách về chủ đề này buộc phải kèm theo các ví dụ. Thông thường, những ví dụ này được chọn sao cho người đọc có thể dễ dàng thử nghiệm trên **công cụ phát triển phần mềm** và **nền tảng phần cứng** giống tác giả. Thật không may, trong lập trình nhúng, điều này không thực tế. Không có gì hợp lý nếu chạy các chương trình ví dụ trên nền tảng mà hầu hết độc giả có—PC, Mac hay Unix workstation.

Ngay cả việc chọn một **nền tảng nhúng tiêu chuẩn** cũng khó khăn, vì như bạn đã biết, không có cái gọi là "hệ thống nhúng điển hình". Bất kể phần cứng nào được chọn, đa số độc giả sẽ không có quyền truy cập. Dù vậy, tôi vẫn cho rằng cần phải chọn một **nền tảng tham chiếu** cho các ví dụ, nhằm giữ cho các ví dụ nhất quán và làm rõ ràng toàn bộ thảo luận.

Để minh họa được nhiều điểm nhất với một phần cứng duy nhất, tôi chọn nền tảng "trung bình" gồm:

- **<mark>bộ xử lý</mark> 16-bit** (Intel 80188EB[2])  
- **128 KB RAM**  
- **256 KB ROM**  
- Một số loại **<mark>ngõ vào</mark>**, **<mark>ngõ ra</mark>** và linh kiện ngoại vi thông dụng

Bo mạch này có tên **Target188EB**, do Arcom Control Systems sản xuất và bán. Thông tin chi tiết và hướng dẫn đặt mua có trong Phụ lục A.

[2] Vi xử lý Intel 80188EB là phiên bản đặc biệt của 80186, được thiết kế lại cho hệ thống nhúng. Bộ xử lý 80186 gốc là người kế nhiệm 8086 được IBM dùng trong máy tính cá nhân đầu tiên (PC/XT). Dù 80186 không bao giờ được dùng làm nền tảng PC (IBM chọn 80286 cho PC/AT), các phiên bản của nó từ Intel và AMD đã rất thành công trong hệ thống nhúng thời gian gần đây.

Nếu bạn có **<mark>phần cứng tham chiếu</mark>**, sẽ dễ dàng chạy hết các ví dụ trong sách. Ngược lại, bạn cần **port** mã nguồn sang nền tảng nhúng bạn có. Mọi nỗ lực đã được thực hiện để chương trình ví dụ **<mark>di động</mark>** nhất có thể. Tuy nhiên, hãy nhớ rằng phần cứng mỗi hệ thống nhúng đều khác nhau, và một số ví dụ có thể không phù hợp với phần cứng của bạn (chẳng hạn driver Flash ở Chương 6 không thể port nếu bo mạch không có Flash).

Trong Chương 5, chúng ta sẽ nói nhiều hơn về phần cứng. Trước hết, chúng ta hãy bắt đầu với một số vấn đề về phần mềm.


*Hết Chương 1*

