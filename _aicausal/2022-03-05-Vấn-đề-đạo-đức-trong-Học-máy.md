---
layout: single
sidebar:
 nav: aicausal
title: Vấn đề đạo đức trong Học máy
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 18"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac18
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 18**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Các mô hình Học máy có vai trò ngày càng quan trọng trong xã hội ngày nay. Trước đây con người đưa ra quyết định và bây giờ thuật toán làm thay. Hệ thống thuật toán này chi phối mọi thứ từ việc chọn lọc những email chúng ta nhận, tới khả năng được phê duyệt tín dụng hay đối tượng mà ta có cơ hội hẹn hò. Có thể nói, tác động của chúng đối với trải nghiệm của con người về thế giới ngày càng lớn. Tuy vậy, hiểu biết của chúng ta về cách thức hoạt động của hệ thống này vẫn chưa đầy đủ. Chúng ta không thể lý giải hay chỉnh sửa khi các thuật toán này đưa ra những dự báo mang tính phân biệt đối xử hoặc những kết quả củng cố cho những thiên kiến sẵn có. May mắn là, suy luận nhân quả cung cấp cho chúng ta một khung lý luận để suy luận về vấn đề này.

**Biểu đồ nhân quả làm cho các giả định trở nên rõ ràng**

Ngay cả lúc chưa sử dụng hết các công cụ của suy luận nhân quả, mỗi khi chúng ta tiếp cận một vấn đề mới, việc cố gắng vẽ ra biểu đồ nhân quả có thể mang lại nhiều thông tin có ích. Điều này buộc ta phải đối mặt với những giả định ta đưa ra về một hệ thống. Đồng thời nó cũng giúp người khác hiểu các giả định mà ta đặt ra và cung cấp một khuôn khổ hợp lý cho tranh luận.

{% include figure image_path="/assets/images/aicausal/chap6/chap6_18_1.png" %} 

Việc làm rõ các giả định của chúng ta giúp tăng cường tính minh bạch. Nhưng nó không bảo vệ ta khỏi các giả định bất hợp lý. Việc thiết lập các mối quan hệ nhân quả thực sự rất khó. Trừ khi chúng ta có thể thực hiện đầy đủ các thí nghiệm để xác thực giả thuyết của mình, lý luận nhân quả từ dữ liệu quan sát thường là các giả định chưa được kiểm chứng (đôi khi không thể kiểm chứng). Chính vì vậy ta cần phải thận trọng khi đưa ra bất kỳ khẳng định nào về nhân quả.  

**Loại bỏ các thuộc tính cần bảo hộ là chưa đủ**

Phân biệt đối xử dựa trên các thuộc tính cần bảo hộ, như chủng tộc hay tình trạng thương tật, bị đánh giá là phi đạo đức, thậm chí là bất hợp pháp ở nhiều nơi. Việc tránh sự phân biệt đối xử trực tiếp (mà theo đó một cá nhân có thuộc tính cần bảo hộ nào đó bị đối xử bất lợi) tương đối dễ dàng. Thông thường, những thuộc tính cần bảo hộ này thường bị loại bỏ khỏi hệ thống học máy.  Việc đưa trực tiếp thuộc tính cần bảo hộ vào mô hình tạo ra sự phân biệt đối xử dựa trên thuộc tính đó.

Tuy nhiên phân biệt đối xử gián tiếp dựa trên nhân quả thường khó phát hiện và khó loại trừ hơn. Nhiều thuộc tính không cần bảo hộ lại có khả năng dự báo tốt thuộc tính cần bảo hộ. Lấy ví dụ, vị trí địa lý có thể tương quan lớn với chủng tộc, tôn giáo và tuổi tác. Khi từ chối khoản cho vay đối với   một cá nhân thuộc mã vùng địa lý cụ thể, ngân hàng thực tế có thể đang gián tiếp phân biệt đối xử một thuộc tính cần bảo hộ.

Một hình thức phân biệt đối xử khác có tên gọi là phân biệt đối xử gián tiếp giả. Đây là những trường hợp không có đường kết nối từ thuộc tính nhân quả tới kết quả đầu ra. Tuy nhiên như đã thấy ở chương trước (“Từ tương quan đến nhân quả”), các mối tương quan có thể phát sinh từ nhiều cấu trúc nhân quả khác nhau. Như vậy, chỉ loại bỏ thuộc tính cần bảo hộ không có nghĩa là đã loại bỏ được tác động của nó. Không thể đảm bảo một hệ thống không phân biệt đối xử dựa trên thuộc tính cần bảo hộ chỉ vì nó không trực tiếp bao gồm thuộc tính đó. Nói một cách dễ hiểu, chỉ vì một đặc tính không gây ra một đối tượng cụ thể không có nghĩa là nó không có khả năng dự báo đối tượng đó. Đây là một thách thức lớn đối với hệ thống thuật toán được thiết kế nhằm tìm ra các mối tương quan tiềm ẩn, đặc biệt trong trường hợp dữ liệu lịch sử dùng để huấn luyện thuật toán có thể bị ảnh hưởng bởi thiên lệch chọn (và một số thiên lệch khác).

Chỉ loại bỏ những thuộc tính cần bảo hộ là chưa đủ, chúng ta cần đánh giá mô hình kết quả dựa trên các thuộc tính công bằng và tính phân biệt đối xử của nó. Có nhiều thước đo cho tính công bằng tuy nhiên rất khó để tối ưu hoá tất cả thước đo.

Một số nghiên cứu đề xuất sử dụng quan hệ nhân để hiểu và xác định tính công bằng cũng như phân biệt đối xử. Cụ thể, nếu ta có một mô hình biểu đồ nhân quả của hệ thống, ta có thể quan sát những đường dẫn nào bị ảnh hưởng bởi các thuộc tính cần bảo hộ và giải thích trách nhiệm của chúng. Một số mô hình nhân quả cấu trúc phi tham số đóng góp cho việc phát hiện và chỉ ra sự khác biệt chính giữa phân biệt đối xử trực tiếp, phân biệt đối xử gián tiếp và phân biệt đối xử giả.

Điều này cho thấy khó khăn nằm ở bước xây dựng biểu đồ nhân quả. Tất nhiên một biểu đồ nhân quả có thể được sử dụng để bao gồm tất cả các thiên kiến, định kiến, nhưng ít nhất nó vẫn cung cấp cơ sở lập luận.

**Bất biến mở ra đường tới công bằng**

Một ý tường thú vị được đề xuất trong phần cuối của bài nghiên cứu về phương pháp Giảm thiểu rủi ro bất biến (IRM): coi các nhóm mà ta muốn có sự công bằng như môi trường. Khi tìm hiểu một mô hình bất biến (ICP hoặc IRM), chúng ta rõ ràng đang cố gắng tìm hiểu một mô hình hoạt động tối ưu trong các môi trường khác nhau. Chúng ta có thể xây dựng các môi trường đó bằng cách tách các nhóm có các giá trị khác nhau cho các thuộc tính cần bảo hộ. Sau đó, bằng cách huấn luyện một mô hình tìm cách hoạt động tối ưu trong từng môi trường, chúng ta có thể đảm bảo hiệu quả tốt nhất cho từng thuộc tính cần bảo hộ. 

Nói cách khác, các thuộc tính bất biến chính là các thuộc tính nhất quán giữa các nhóm. Hãy xem xét một ví dụ nữa, khi ngân hàng cấp các khoản vay trực tiếp cho cá nhân, và không muốn phân biệt đối xử khách hàng dựa trên các thuộc tính cần bảo hộ. Bằng cách chia khách hàng vào các nhóm theo các thuộc tính cần bảo hộ, ngân hàng đang tìm cách để hiểu liệu điều gì tác động đến các khoản vay xấu trên tất cả các nhóm. 

Ý tưởng về việc học một thuộc tính dự báo bất biến trên nhiều môi trường nghĩa là chúng ta sử dụng một dạng biểu diễn thực sự phản ánh mô hình tạo lập dữ liệu. Dạng biểu diễn này, ở một mức độ nào đó, có thể phân tách, theo nghĩa là mỗi chiều của dạng biểu diễn (một vectơ) phải tương ứng với một đại lượng có ý nghĩa. Trong bài nghiên cứu về tính công bằng của biểu diễn có tính phân tách, chứng minh bằng thực nghiệm cho thấy cách biểu diễn này cải thiện tính công bằng trong các ứng dụng thực tiễn.  


