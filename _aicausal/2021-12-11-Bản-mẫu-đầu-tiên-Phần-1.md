---
layout: single
sidebar:
 nav: aicausal
title: Bản mẫu đầu tiên - Phần 1
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 14"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac14
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 14**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Sự hứa hẹn của phương pháp Giảm thiểu rủi ro bất biến (IRM) thật hấp dẫn: cải thiện khả năng khái quát hoá ngoài phân phối nhờ vào việc sử dụng biểu diễn dữ liệu gần với các mối tương quan nhân quả thực. Bài nghiên cứu về IRM đã thực hiện một số thử nghiệm chứng minh phương pháp này hoạt động hiệu quả khi áp dụng với mô hình cấu trúc nhân quả nhân tạo. Không chỉ vậy, một thử nghiệm trong đó tương quan giả được đưa vào tập dữ liệu MNIST (bằng cách tô màu hình ảnh) cũng đã được thực hiện và mô tả cụ thể.

Để hiểu rõ hơn về thuật toán, chúng ta muốn thử nghiệm phương pháp tương tự trên một trường hợp ít yếu tố nhân tạo hơn: một tập dữ liệu hình ảnh tự nhiên.

**Bộ dữ liệu iWildcam**

Bộ dữ liệu [iWildCam 2019](https://www.kaggle.com/c/iwildcam-2019-fgvc6)  (từ Thử thách iWildCam 2019) bao gồm hình ảnh các loài thú hoang được đón chụp tự đồng bằng máy ảnh chuyên dụng. Tập dữ liệu có tên Caltech Camera Traps (CCT) bao gồm 292.732 hình ảnh, mỗi hình được gắn nhãn 1 trong 13 loài thú sẵn có, hoặc không loài nào. Các hình ảnh được thu thập từ 143 địa điểm trong nhiều điều kiện thời tiết và thởi điểm khác nhau trong ngày. Thử thách đặt ra là nhận diện loài thú xuất hiện trong bức ảnh.


{% include figure image_path="/assets/images/aicausal/chap4/chap4_14_1.png" caption="Trái, một con sói đồng cỏ Bắc Mỹ trong môi trường tự nhiên. Phải, một con gấu mèo ở cùng một địa điểm vào ban đêm. Nguồn hình ảnh: Thử thách iWildCam 2019.
" %}

**Thiết lập thử nghiệm**

Thiết lập này vốn khá tương đồng với sự phân chia môi trường trong IRM. Mỗi vị trí đặt máy ảnh là một môi trường vật lý riêng biệt và gần như nhất quán với các chu kì mùa vụ,, thời tiết, ngày/đêm . Không có hai môi trường nào hoàn toàn giống nhau mặc dù các máy ảnh được đặt rải rác quanh một khu vực địa lý (phía Tây Nam Mỹ).

Đối tượng mục tiêu trong tập dữ liệu là các loài thú, về cơ bản là bất biến trong các môi trường, một con gấu mèo trên núi sẽ có những đặc điểm giống với một con gấu mèo ở sân sau nhà bạn. Các hình ảnh phân bố không đồng đều giữa các môi trường vì  các con thú xuất hiện nhiều ở một số địa điểm hơn các nơi khác. Các loài thú cũng phân bố không đều theo máy ảnh: một số máy sẽ chủ yếu chụp được một số loài nhất định, tuỳ thuộc vào tập tính của từng loài trên địa bàn.

Nếu chỉ đơn thuần huấn luyện mô hình nhằm tối thiểu hóa rủi ro thực nghiệm trên một tập con các máy ảnh, thì chúng ta đang để mô hình học sự mất cân bằng trong dữ liệu. Nếu 99% hình ảnh từ máy ảnh 1 được gắn nhãn là hươu, thì chúng ta có thể có mô hình phân loại chính xác đến 99% bằng cách học nhận diện một cái cây đổ chỉ có trong máy ảnh 1 chứ không phải hươu. Rõ ràng một mô hình phân loại như vậy không thực sự học cách nhận diện hươu và sẽ trở nên vô dụng khi áp dụng vào môi trường khác. 

Chúng ta muốn máy tự nhận diện loài vật.. Thiết lập IRM dường như rất phù hợp để giải quyết thách thức này. 

Để đánh giá cách tiếp cận này, chúng ta giới hạn thử nghiệm với ba máy ảnh và hai loài động vật được chọn ngẫu nhiên. Trong số 3 máy ảnh, 2 máy ảnh được sử dụng làm môi trường huấn luyện và một máy ảnh còn lại là môi trường đánh giá. Nhiệm vụ trở thành bài toán phân loại nhị phân: phân biệt sói đồng cỏ và gấu mèo. Để giải quyết bài toán, mô hình phân loại ResNet18, được huấn luyện trước trên tập dữ liệu lớn ImageNet, được sử dụng để trích xuất các đặc trưng cho một mạng thần kinh kết nối toàn phần gắn với đầu ra có dạng hàm sigmoid.

Mỗi một môi trường đều chứa cả hình ảnh của sói đồng cỏ và gấu mèo. Ngay cả tập dữ liệu thu gọn này cũng cho thấy một số thách thức điển hình ở các bài toán thị giác máy tính trong thực tế: một số hình ảnh bị tối, bị mờ, một số được gắn nhãn là có thú khi chỉ nhìn thấy chân của chúng, hay một số không có gì ngoài một mảng lông bao phủ ống kính. Một số phương pháp thành công đơn giản bằng việc bỏ qua những điểm này, nhưng cuối cùng vẫn phải chọn thủ công những hình ảnh hiển thị rõ ràng một con sói đồng cỏ hay một con gấu mèo có thể nhận dạng được.

**Kết quả**

Khi giải quyết bất kỳ bài toán học giám sát nào, việc thiết lập một mô hình cơ sở đơn giản để so sánh  hiệu năng của các mô hình là một ý tưởng tốt. Với bài toán phân loại nhị phân, một mô hình cơ sở thích hợp có thể là mô hình luôn luôn dự đoán loại nhãn chiếm đa số của tập huấn luyện. Ba môi trường có nhãn dán phân bố như bảng dưới đây. Trong hai môi trường huấn luyện nhãn dán sói đồng cỏ chiếm đa số, vì vậy độ chính xác cơ sở sẽ bằng với độ chính xác khi mô hình luôn dự đoán con thú trong bức hình là sói đồng cỏ bất kể môi trường và hình ảnh đầu vào.


{% include figure image_path="/assets/images/aicausal/chap4/chap4_14_2.png" %}

Khi giải quyết bài toán bằng Tối thiểu hóa rủi ro thực nghiệm trên một tập dữ liệu hữu hạn (Empirical Risk Minimization – ERM) (bằng việc tối thiểu hoá entropy chéo giữa các loại nhãn dán), chúng ta nhận thấy mô hình hoạt động tốt trong môi trường huấn luyện nhưng kém trong môi trường đánh giá. Các chỉ số đo lường hiệu năng của mô hình sau 120 lượt huấn luyện (epoch) được ghi lại trong bảng dưới đây. Độ chính xác cao nhất trong môi trường huấn luyện đạt được ở lượt huấn luyện thứ 40, sau đó ERM bắt đầu quá khớp (overfit). Đối với IRM, chúng ta cần đánh đổi một chút độ chính xác ở tập huấn luyện để đạt được kết quả tốt hơn nhiều ở tập đánh giá, độ chính xác thử nghiệm cao nhất đạt được ở lượt huấn luyện thứ 120.

{% include figure image_path="/assets/images/aicausal/chap4/chap4_14_3.png" caption="Bảng so sánh các chỉ số trên tập huấn luyện kết hợp và tập đánh giá của hai phương pháp ERM và IRM.
" %}

Có thể thấy ERM hoạt động tốt hơn mô hình cơ sở trong mọi môi trường, nhưng không hơn quá nhiều trong môi trường đánh giá. Lý do có thể bởi mô hình đã học các tương quan giả. Mô hình có thể phân biệt hiệu quả giữa hai loại nhãn dán là sói đồng cỏ và gấu mèo trong môi trường huấn luyện nhưng các thuộc tính mà nó dựa vào chưa đủ sức khái quát để dự đoán trong môi trường đánh giá.

Trái lại, IRM chỉ để mất 1% độ chính xác trong môi trường huấn luyện để đổi lại mức độ hoạt động tốt ngang ngửa trong môi trường đánh giá. IRM đã thiết lập biểu diễn thuộc tính có thể chuyển đổi một cách hiệu quả giữa các môi trường khác nhau, đồng thời cũng chứng minh nó là mô hình phân loại hiệu quả.

Thực tế, chúng ta nhận thấy IRM hoạt động tốt nhất khi điểm phạt bổ sung của IRM không được thêm vào hàm tổn thất cho đến khi ERM đạt mức tối ưu –lượt huấn luyện thứ 40 trong ví dụ trên. Như vậy, ERM và IRM có cách thức huấn luyện và hiệu quả tương tự nhau cho đến tận điểm đó. Khi điểm phạt được đưa vào IRM, IRM tiếp tục học và đạt được khả năng khái quát hoát ngoài phân phối trong khi ERM bị quá khớp. Đến lượt huấn luyện thứ 120, IRM có độ chính xác lần lượt là 85% và 79% ở tập huấn luyện và tập đánh giá, trong khi đó, ERM tuy đạt được độ chính xác 91% trong các môi trường huấn luyện kết hợp nhưng đánh đổi bằng việc độ chính xác thấp trong môi trường đánh giá, chỉ đạt 33%. 

