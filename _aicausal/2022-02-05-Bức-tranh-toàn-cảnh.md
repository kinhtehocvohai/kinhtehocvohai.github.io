---
layout: single
sidebar:
 nav: aicausal
title: Bức tranh toàn cảnh
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 16"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac16
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 16**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Quan hệ nhân quả bao quát nhiều lĩnh vực, chủ đề. Ví dụ sử dụng góc nhìn nhân quả để cải thiện các phương pháp học máy, cải tiến nó cho dữ liệu nhiều chiều và  sử dụng chúng để hỗ trợ việc ra quyết định tốt hơn dựa trên dữ liệu trong nhiều bối cảnh thực tế. Trong phần trước (Nhân quả và Bất biến), chúng ta đã thảo luận tại sao dữ liệu được thu thập ít khi phản ánh chính xác tổng thể, do đó khó có thể khái quát chúng trong các môi trường khác nhau hoặc cho các bộ dữ liệu mới. Các phương pháp dựa trên bất biến có tiềm năng trong việc giải quyết vấn đề khái quát hoá bên ngoài phân phối. 

**Lĩnh vực áp dụng**
Như đã đề cập ở chương trước, IRM (Giảm thiểu rủi ro bất biến) đặc biệt phù hợp với các vấn đề phân loại hình ảnh trong các môi trường vật lý đa dạng. Tuy nhiên, môi trường không chỉ gói gọn trong cảnh vật trong một bức hình, và cũng không nhất thiết phải bị cố định với một loại dữ liệu duy nhất. Sau đây chúng tôi sẽ đề cập đến một vài lĩnh vực ứng dụng ngoài thị giác máy tính.

**Y học**
Trong y học, hình ảnh y khoa cần được các bác sĩ X-quang chú thích để xác định các biểu hiện bất thường. Những hình ảnh được chú thích này sau đó được sử dụng để huấn luyện và xây dựng các mô hình chẩn đoán. Nhiều khi các thiết bị (như máy quét MRI) dùng để tạo ra những hình ảnh y khoa có thể hoạt động không đồng đều.  Do khác biệt về cấu hình cơ học, nhà cung cấp hay các lý do khác, hình ảnh được tạo ra bởi một máy quét MRI có thể sai khác một cách có hệ thống so với máy quét khác cho cùng một bệnh nhân. Do đó, mô hình chẩn đoán được xây dựng dựa trên hình ảnh được tạo bởi máy quét MRI cũ có thể hoạt động không tốt khi được thử nghiệm trên hình ảnh được tạo bởi máy quét mới. Một trong những cách để giải quyết vấn đề này là yêu cầu các bác sĩ X-quang chú thích các hình ảnh được tạo bởi máy quét mới và sau đó huấn luyện lại mô hình. Tuy vậy điều này rất tốn kém và mất thời gian. Hơn nữa, đây không phải là một giải pháp lâu dài, bởi mỗi khi có máy quét mới hoặc thay đổi cấu hình, mô hình cần phải được huấn luyện lại với một bộ dữ liệu hình ảnh hoàn toàn mới. 

Mô hình chẩn đoán dựa trên dự báo bất biến coi các máy quét như các môi trường có thể loại trừ các khác biệt do máy móc và thay đổi các quyết định của nó cho phù hợp. Giải pháp này có thể tiết kiệm phần lớn thời gian và tiền bạc cần thiết để chú thích hình ảnh từ máy quét mới.

**Kỹ thuật robot**

{% include figure image_path="/assets/images/aicausal/chap5/chap5_16_1.png" caption="Các hệ thống tự hành được huấn luyện trong phòng thí nghiệm hoặc môi trường hạn chế sẽ gặp khó khăn khi phải thích ứng với sự đa dạng của thế giới thực.
" %} 

Các hệ thống tự hành phải phát hiện và thích ứng với các môi trường khác nhau. Các hệ thống này dựa vào các cảm biến máy ảnh tinh vi và một lượng lớn các dữ liệu đa dạng đã được gắn nhãn từ thế giới thực (thường khó để thu thập). Có thể lấy ví dụ như nhiệm vụ tự động đi theo đường mòn được tạo bởi những người leo núi hoặc đạp xe vượt địa hình. Đây là một nhiệm vụ gần như vẫn còn nan giải với công nghệ robot, nhưng đặc biệt quan trọng trong các lĩnh vực ứng dụng như tìm kiếm và cứu hộ.

Tuy nhiều loại robot (như robot bốn chân) có thể di chuyển hiệu quả, việc điều hướng thành công vào các đường mòn vào rừng trong thế giới thực vẫn là nhiệm vụ khó khăn. Không chỉ vậy, việc nhận biết các đường mòn cũng không hề đơn giản. Diện mạo của địa hình hoang dã có thể thay đổi rất nhiều tuỳ thuộc vào vị trí, đường không trải nhựa thường không có cấu trúc (và dễ bị lẫn vào khu vực cây cỏ xung quanh), và chúng thay đổi theo thời gian. Dường như là bất khả thi để có một bộ dữ liệu toàn diện về tất cả các con đường mòn trong mọi điều kiện thời tiết và ánh sáng.

Trong những trường hợp như vậy, một giải pháp khả thi là coi bài toán nhận biết đường mòn như bài toán phân loại hình ảnh và áp dụng phương pháp dựa trên bất biến hoạt động trực tiếp trên các giá trị điểm ảnh của ảnh gốc. Áp dụng thành công có thể cho phép khái quát hoá ngoài phân phối đối với các đường mòn mới, bởi tính năng đã được học có tính chuyển đổi tốt hơn so với các đặc tính riêng của từng môi trường cụ thể. Những ý tưởng tương tự như vậy cũng có tiềm năng áp dụng cho xe tự lái trong khu vực đô thị. 

**Hệ thống ghi nhận hoạt động**

Các thiết bị thông minh (điện thoại, đồng hồ, thiết bị theo dõi thể dục) gồm một loạt các cảm biến. Việc phân loại dữ liệu này theo hoạt động đang được thực hiện tại thời điểm ghi nhận, ví dụ như đang ngồi, đứng hay bơi, cho pháp phát triển các hệ thống ghi nhận hoạt động của con người dựa trên học máy. Dự báo chính xác hoạt động của người sử dụng thiết bị mang đến nhiều lợi ích trong nhiều trường hợp, đặc biệt là về sức khoẻ và tinh thần. 

Tuy nhiên, rất khó để mô hình hoá dữ liệu này một cách thoả đáng bởi tính đa dạng trong thế giới thực. Mỗi cá nhân có thể thực hiện một hoạt động cụ thể ngày qua ngày hơi khác một chút, hoặc thiết bị có thể được đặt ở những vị trí bất thường hay được đeo theo nhiều hướng khác nhau. Tất nhiên, những người dùng khác nhau cũng có những đặc điểm thể chất khác nhau, và bản thân các thiết bị cũng có những sự khác biệt về cảm biến và hệ thống điều hành. Điều này có nghĩa là chúng ta cần một tập dữ liệu đã được gắn nhãn ghi lại hoạt động của từng người dùng và thiết bị (điều này vô cùng tốn kém) hoặc một cách khác để xác định các thuộc tính tổng quát tốt hơn. Các phương pháp dựa trên bất biến có thể đặc biệt hữu ích và rất phù hợp trong trường hợp này, nắm bắt bản chất của hành động, ví dụ như “ngồi”, thay vì kích hoạt cảm biến cụ thể cho một người dùng cụ thể đang ngồi trên một chiếc ghế cụ thể.

**Xử lý ngôn ngữ tự nhiên**

{% include figure image_path="/assets/images/aicausal/chap5/chap5_16_2.png" caption="Môi trường có ở khắp mọi nơi. Ví dụ, các ngôn ngữ tự nhiên trên khắp thế giới.
" %} 


Các phương pháp dự đoán bất biến không chỉ giới hạn trong các vấn đề liên quan tới hình ảnh. Trong xử lý ngôn ngữ tự nhiên, việc phân tích các văn bản từ các nền tảng xuất bản khác nhau có thể phức tạp bởi sự khác biệt về bối cảnh, cách dùng từ cũng như phong cách tác giả. Ví dụ như các bài báo về tài chính thường sử dụng những từ ngữ và giọng điệu khác với các bài báo về văn hoá, xã hội. Các bài báo về tài chính thường ngắn gọn trong khi các bài về văn hoá xã hội thường mang tính giải trí hoặc dấu ấn cá nhân. Tương tự, các đánh giá sản phẩm trực tuyến cũng khác với những dòng tweet. Phân tích cảm xúc của người viết cũng dựa nhiều vào ngữ cảnh, các từ khác nhau được sử dụng để thể hiện sở thích của một cá nhân, ví dụ, liệu người đó thích sách hay thiết bị điện tử.

Hai bài báo gồm “Nghiên cứu thực nghiệm về Giảm thiểu rủi ro bất biến” và “Hợp lý hoá bất biến” đã áp dụng ý tưởng của IRM vào phân tích cảm xúc, và nhận thấy sự cải thiện khả năng khái quát hoá ngoài phân phối. Đặc biệt, bất biến hoạt động để loại bỏ các tương quan giả có thể có giữa một từ cụ thể với mục tiêu. Giống như hình ảnh, kho dữ liệu văn bản tạo thành tập dữ liệu nhiều chiều (bởi có rất nhiều từ) làm cho khó phát hiện các mối tương quan giả một cách thủ công. Do đó, việc áp dụng phương pháp dựa trên bất biến có tiềm năng rất lớn. 

**Hệ thống đề xuất**

{% include figure image_path="/assets/images/aicausal/chap5/chap5_16_3.png" caption="Dữ liệu một hệ thống đề xuất thu thập được về cơ bản đã bị thiên lệch bởi chính các đề xuất mà nó đưa ra. Chúng ta có thể giải quyết thiên lệch này bằng suy luận nhân quả.
" %}

Hệ thống đề xuất là các thuật toán được thiết kế để hiện thị các mục liên quan cho người dùng trên trang web (ví dụ: bộ phim nên xem, sách nên đọc hay sản phẩm nên mua). Do đó, việc đưa ra các đề xuất tốt là một nhiệm vụ quan trọng: chúng ta muốn đưa ra những đề xuất phù hợp cho người dùng dựa trên những ghi nhận về lịch sử hoạt động của họ, từ đó suy ra sở thích của họ.

Dữ liệu huấn luyện có thể rõ ràng (như đánh giá của người dùng về sản phẩm) hoặc tiềm ẩn (như thời gian ở lại web hay số lần nhấp chuột vào sản phẩm). Một vấn đề phổ biến đối với hệ thống đề xuất là: người dùng về cơ bản không thể nhấp vào một mục không được đề xuất. Mô hình hoá dữ liệu mà không suy xét đến điều này cũng giống như giả định dữ liệu độc lập và được phân phối giống nhau, là không chính xác: người dùng không chọn các mục ngẫu nhiên và độc lập với nhau. Ví dụ, người dùng sẽ chọn một trong hai bộ phim cạnh tranh với nhau để xem, hơn là chọn có nên xem từng bộ phim một cách độc lập hay không. 

RecSys là một ứng dụng cổ điển cho quan hệ nhân quả, cho phép sửa chữa thiên lệch tiếp xúc này bằng cách coi việc lựa chọn các mục để đề xuất cho người dùng như một can thiệp. Áp dụng các phương pháp tiếp cận nhân quả để đưa ra đề xuất một cách tự nhiên sẽ tăng tính khái quát hoá cho dữ liệu mới, và dường như các phương pháp sử dụng dự báo bất biến có thể cải thiện điều này.
