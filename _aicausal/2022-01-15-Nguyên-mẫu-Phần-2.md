---
layout: single
sidebar:
 nav: aicausal
title: Nguyên mẫu - Phần 2
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 15"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac15
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 15**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

**Diễn giải mô hình**

IRM cho kết quả ấn tượng, nhất là khi tính đến sự khó khăn trong việc “học” từ các hình ảnh [ở phần trước]. IRM tạo ra sự cải thiện rõ ràng đáng kể so với ERM khi được đặt vào môi trường mới. Trong phần này, chúng ta sẽ cùng xem xét một vài ví dụ cụ thể về những trường hợp thành công và thất bại của mô hình nguyên mẫu và suy đoán xem tại sao lại như vậy.

Sẽ thật tuyệt nếu ta hiểu rõ hơn liệu IRM có học được các đặc tính bất biến hay không. Điều này có nghĩa là liệu IRM có học được cách phát hiện ra một bộ phận trên cơ thể của loài thú hoang thay vì địa hình trong ảnh. Sẽ rất hữu ích nếu ta hiểu được phần nào của hình ảnh đóng góp vào hiệu năng của IRM. Có thể thấy nhiệm vụ phân loại vốn không hề dễ dàng: nếu nhìn vào một số hình ảnh trong tập dữ liệu Wildcam, ngay từ ban đầu, chúng ta bằng mắt thường thậm chí còn khó chỉ ra chính xác đâu là thú hoang cần được phân loại. Một kỹ thuật dùng để diễn giải như LIME (Phép diễn giải cục bộ cho mô hình bất khả tri) có thể cung cấp cho chúng ta một vài thông tin cụ thể và có hữu ích về cách mô hình phân loại hoạt động.

LIME là một kỹ thuật diễn giải có thể áp dụng cho hầu hết mọi loại mô hình phân loại, và ở đây chúng ta sẽ xem xét ứng dụng của nó đối với dữ liệu hình ảnh. Cụ thể, LIME dùng để hiểu từng thông tin đầu vào có ảnh hưởng như thế nào đến đầu ra của mô hình. Về cơ bản, điều này có thể thực hiện bằng cách lần lượt thay đổi dữ liệu đầu vào và quan sát ảnh hưởng của nó trên đầu ra.

Hãy cùng quan sát cách LIME hoạt động thông qua một ví dụ cụ thể là hình ảnh mẫu trong tập đánh giá, cụ thể, hiểu được các yếu tố đầu vào cần cung cấp và kết quả đầu ra mong đợi. Hình bên trái dưới đây là ảnh gốc của một con sói đồng cỏ với kích thước chiều cao=747 và chiều rộng=1024, giống như tất cả các hình ảnh khác trong tập dữ liệu.



{% include figure image_path="/assets/images/aicausal/chap4/chap4_15_1.png" caption="Hình bên trái: Hình ảnh Wildcam gốc. Hình bên phải: Hình ảnh đã được cắt và chia tỷ lệ lại theo yêu cầu của ResNet18
" %}

Để sử dụng IRM, trước tiên cần thực hiện một số thao tác xử lý hình ảnh như chỉnh sửa kích thước, cắt hình ảnh, hay chuẩn hoá – giống như các thao tác xử lý khi huấn luyện mô hình. Cuối cùng ta thu được hình ảnh đầu vào như hình bên phải ở trên, một hình ảnh 224x224 đã được chuẩn hoá. Hình ảnh sau xử lý được mô hình IRM dự đoán 98%  (0,98) là sói đồng cỏ. Có thể thấy, mô hình khá chắc chắn về dự đoán này.

Bây giờ, hãy xem LIME hoạt động như thế nào trong trường hợp này. Đầu tiên, LIME xây dựng một mô hình tuyến tính cục bộ và đưa ra dự báo cho hình ảnh. Đối với hình ảnh sói đồng cỏ trong ví dụ này, kết quả dự báo là 0,95 – khá gần với IRM. Để diễn giải dự báo này, LIME sử dụng các dạng biểu diễn có thể diễn giải được. Đối với dữ liệu hình ảnh,  dạng biểu diễn có thể diễn giải được về cơ bản là các nhóm điểm ảnh (pixel) liền kề tương tự nhau, hay còn được gọi là các siêu điểm ảnh (superpixel). Các siêu điểm ảnh được tạo ra bởi một thuật toán tiêu chuẩn, QuickShift, trong quá trình triển khai LIME. Hình bên trái phía dưới hiển thị toàn bộ 34 siêu điểm ảnh của hình ảnh trong ví dụ.



{% include figure image_path="/assets/images/aicausal/chap4/chap4_15_2.png" caption="LIME ẩn đi những tổ hợp ngẫu nhiên của các siêu điểm ảnh, được tạo ra bởi QuickShift, để xây dựng một mô hình tuyến tính cục bộ
" %}

Sau đó, LIME tạo ra các dị bản của ảnh gốc bằng cách che đi các tổ hợp khác nhau của các siêu điểm ảnh (ví dụ trong hình trên là các superpixel ở giữa góc phải phía trên). Mỗi tổ hợp ngẫu nhiên của các superpixel bị che đi là một chi tiết dị bản của hình ảnh gốc. Chúng ta có thể chọn số lượng chi tiết dị bản, 1000 trong trường này. Tiếp đến, LIME xây dựng mô hình hồi quy dựa trên tất cả các ảnh dị bản này và xác định các siêu điểm ảnh đóng góp nhiều nhất vào dự báo, dựa trên trọng số của chúng.

Hình dưới đây cho thấy khả năng diễn giải của các siêu điểm ảnh (với phần còn lại của hình ảnh được tô xám) cho 12 đặc tính đóng góp hàng đầu vào việc dự đoán phân loại sói đồng cỏ. Tuy khá nhiều đặc tính chủ yếu gây nhiễu như tán lá hoặc địa hình, một trong số chúng bao gồm toàn bộ cơ thể của sói đồng cỏ. Nghiên cứu những giải thích này cung cấp một cách đánh giá khác về IRM và có thể làm tăng sự tin cậy vào khả năng học các đặc tính tốt của mô hình.


{% include figure image_path="/assets/images/aicausal/chap4/chap4_15_3.png" caption="Các siêu điểm ảnh không bị tô xám là 12 siêu điểm ảnh đóng góp hàng đầu vào phân loại sói đồng cỏ cho mô hình IRM
" %}

Tương tự, chúng ta cũng dùng LIME tạo ra 12 siêu điểm ảnh hàng đầu giải thích cho cùng một hình ảnh nhưng dựa trên mô hình ERM. Có thể thấy chúng dường như bao gồm nhiều cảnh vật xung quanh hơn bất cứ bộ phận cơ thể nào của sói đồng cỏ.

{% include figure image_path="/assets/images/aicausal/chap4/chap4_15_4.png" caption="Các siêu điểm ảnh không bị tô xám tương ứng với 12 siêu điểm ảnh hàng đầu đóng góp vào phân loại sói đồng cỏ cho mô hình ERM. Trong trường hợp này, chúng hầu như không bao gồm các bộ phận cơ thể của sói đồng cỏ
" %}

Tuy nhiên, có những trường hợp mà diễn giải của LIME dựa trên các đặc tính nhiễu. Ví dụ như trong hình bên dưới, hình gốc được IRM phân loại là sói đồng cỏ với xác suất 72% (0,72) trong khi điểm LIME xấp xỉ 0,53. Trong trường hợp này các siêu điểm ảnh đóng góp vào việc phân loại cho cả IRM và ERM thường bao gồm địa hình hoặc tán lá, mặc dù có một số ít chạm tới phần thân ngoài của sói đồng cỏ. 

{% include figure image_path="/assets/images/aicausal/chap4/chap4_15_5.png" caption="Trong ví dụ này, cả IRM và ERM dường như đều dựa vào các đặc tính của môi trường để dự đoán
" %}

Chúng ta có thể nhận thấy rằng các giải thích có ý nghĩa trực quan hơn khi dự đoán của mô hình tuyến tính cục bộ của LIME gần với dự báo của IRM.

IRM chỉ có thể học các đặc tính bất biến mà môi trường mã hoá. Nếu có các tương quan giả giống nhau giữa các môi trường, IRM sẽ không phân biệt được chúng với các đặc tính bất biến.

Một đặc tính dường như bất biến trong tập dữ liệu này là chu kỳ ngày hoặc đêm. Gấu mèo chỉ xuất hiện vào ban đêm và IRM có thể dựa rất nhiều vào đặc tính này để nhận diện hình ảnh gấu mèo. Mối tương quan này là giả bởi một con gấu mèo vẫn là một con gấu mèo bất kể ngày hay đêm! Tuy nhiên, chúng ta sẽ cần nhiều môi trường hơn, bao gồm cả hình ảnh của gấu mèo vào ban ngày, để giải quyết vấn đề đó.

Biểu diễn mà IRM trích xuất từ một môi trường về mặt lý thuyết nên gần với với việc mã hoá cấu trúc nhân quả tiềm ẩn của vấn đề hơn ERM. Trong kịch bản lý tưởng, chúng ta có thể kỳ vọng IRM học cách tập trung hơn vào loài động vật trong ảnh, vì sự hiện diện của loài động vật nhất định tương ứng với một nhãn dán nhất định. Các loài động vật ít thay đổi giữa các môi trường, trong khi các đặc điểm môi trường (như tán lá) hoàn toàn khác nhau ở các vị trí đặt bẫy khác nhau. Do đó, các đặc tính nhân quả phải bất biến giữa các môi trường.

Như vậy, mặc dù phương pháp IRM là khá hứa hẹn đối với một số mẫu, nhưng cũng rất khó để xác nhận các quy luật hình ảnh rõ ràng với cả mô hình phân loại và mô hình giải thích. Chúng tôi chỉ huấn luyện lớp cuối cùng của ResNet18 cho IRM. Quyết định này có một nhược điểm: khả năng học tính năng thấp. Do vậy, rất khó để kỳ vọng kết quả đầu ra hoàn hảo, bởi nhiều khả năng các biểu diễn được huấn luyện trước đó bởi ResNet không phù hợp hoàn toàn với gấu mèo và sói đồng cỏ.
 
Không chỉ vậy, mặc dù sự giải thích cho một hình ảnh riêng lẻ phần nào bảo chứng cho chất lượng mô hình, nhưng có lẽ vẫn chưa đủ để vẽ ra bức tranh toàn thể về loại đặc tính mà một mô hình nhất định đang sử dụng, được tổng hợp từ tất cả các sự giải thích riêng lẻ. Mặc dù sự giải thích cho nhiều hình ảnh cung cấp một cái nhìn sâu sắc hơn, nhưng chúng phải được lựa chọn một cách thận trọng. Khi đề cập đến dữ liệu văn bản hoặc dữ liệu dạng bảng, có nhiều cách để xác định tầm quan trọng của các đặc tính tổng thể, vì các đặc tính trong dữ liệu văn bản hay bảng luôn nhất quán trên tất cả các điểm dữ liệu. Ngược lại, các siêu điểm ảnh của một hình ảnh không thể nhất quán trên tất cả hình ảnh, điều này khiến cho việc đánh giá liệu các giải thích có hợp lý hay không thực sự khó khăn. Chính vì vậy, nhiệm vụ phát triển các công cụ để hiểu các tập dữ liệu hình ảnh lớn đòi hỏi một sự nỗ lực đáng kể!

Bạn có thể đọc bản báo cáo đầy đủ về cách áp dụng cũng như kết quả của IRM cho ví dụ phân loại hình ảnh [tại đây](https://scene.fastforwardlabs.com/)
