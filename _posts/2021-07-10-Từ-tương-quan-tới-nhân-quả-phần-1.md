---
layout: single
sidebar:
 nav: aicausal
title: Từ Tương Quan Tới Nhân Quả - Phần 1
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 4"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac04
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 4**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

**Tương quan giả** 

Chắc hẳn chúng ta đã ít nhất một lần thấy những sự kiện thể hiện sự tương quan trong thực tế. Gà trống gáy khi mặt trời mọc. Hoặc đơn giản đèn sẽ tắt khi bạn gạt công tắc. Hay vĩ mô hơn, nhiệt độ Trái Đất đang tăng lên một cách báo động kể từ những năm 1800 trong khi cướp biển lại gần như biến mất! Tương quan có là một kết quả của quan hệ nhân quả, như trong trường hợp bạn gạt công tắt. Tuy nhiên nó không phải lúc nào cũng bao hàm quan hệ nhân quả, như mối quan hệ giữa sự biến mất của cướp biển và tình trạng Trái Đất ấm lên.

Có rất nhiều ví dụ thú vị về mối quan hệ tương quan không bao hàm nhân quả. Đã bao giờ bạn nghe tới Lý thuyết về chiều dài váy hay chỉ số Hemline Index bắt nguồn từ những năm 1920. Lý thuyết này cho rằng tồn tại mối quan hệ tương quan giữa độ dài váy và sự biến động của thị trường chứng khoán. Váy ngắn có xu hướng xuất hiện vào thời điểm niềm tin và cảm giác phấn khích của người tiêu dùng đang ở mức cao, hay thời điểm thị trường đang tăng giá. Ngược lại, váy dài sẽ phổ biến hơn trong thời điểm thị trường u ám hay mọi thứ đang giảm giá. Mặc dù vẫn có những người tin vào lý thuyết này, nhưng hầu hết các nhà phân tích và đầu tư nghiêm túc vẫn ưa thích sử dụng các yếu tố cơ bản của thị trường và dữ liệu kinh tế. 


{% include figure image_path="/assets/images/aicausal/chap3/ac04.png" caption="Minh hoạ Lý thuyết chiều dài váy từ Fashionblogga"%}


Tương quan giả có thể phát sinh do kích thước mẫu nhỏ và sự trùng hợp nhất định xảy ra khi so sánh. Trong thực tế, tương qua giả có thể gây ra những vấn đề nghiêm trọng về mặt đạo đức. Ví dụ, một số đặc tính nhất định có thể gắn liền với các cá nhân hoặc nhóm thiểu số, và những đặc tính này mang tính dự báo cao. Vì vậy việc mô hình coi những đặc tính này là quan trọng có thể gây ra thiên lệch và bất công. 

Theo EducationData.org, vào năm 2019, những người da trắng trong độ tuổi 25-29 có khả năng tốt nghiệp đại học cao hơn 55% so với những người da đen. Dữ liệu cho thấy chủng tộc có tác động đến tỷ lệ tốt nghiệp. Tuy nhiên, không phải chủng tộc tác động năng lực học vấn. Ở đây tồn tại tác động của một biến số thứ ba tiềm ẩn, ví dụ phân biệt chủng tộc. Phân biệt chủng tộc tác động đến người da màu khiến họ gặp bất lợi về mặt giáo dục và kinh tế, ví dụ trường học không dành cho người da trắng nhận được ít tài trợ hơn, cha mẹ không phải người da trắng được trả lương thấp  hơn và ít thời gian quan tâm tới việc giáo dục con cái. Như vậy nếu việc phân tích, nghiên cứu dựa trên tương quan giả là trình độ học vấn và chủng tộc trong trường hợp này có thể gây ra những kết luận thiếu chính xác và không công bằng. 

**Nguyên Lý Đồng căn (nguyên nhân chung)**

Đến đây phần nào ta đã thấy được những tai hại khi phân tích dựa vào tương quan giả. Bây giờ là lúc cần thảo luận về việc tương quan có thể phát sinh từ quan hệ nhân quả như thế nào. Việc này sẽ được thực hiện trong khuôn khổ Mô hình Nhân quả cấu trúc (Strutural Causal Model - SCM). SCM là một biểu đồ phi chu trình có hướng (Directed Acyclic Graph) thể hiện mối quan hệ giữa các biến. Các nút đại diện cho các biến và các cạnh có hướng nối các nút lại với nhau thể hiện mối quan hệ nhân quả. Giá trị của mỗi biến chỉ phụ thuộc và các nút cha mẹ trong biểu đồ (các nút có liên kết trực tiếp với nó), và một biến nhiễu bao gồm các tương tác khác không được đưa vào trong mô hình. Trước khi xem xét ba cấu trúc nhân quả, chúng ta hãy cùng tìm hiểu một số thuật ngữ sau:
- Biểu đồ nhân quả là biểu đồ phi chu trình có hướng biểu thị sự phụ thuộc giữa các biến.
- Mô hình Nhân quả cấu trúc cung cấp nhiều thông tin hơn một biểu đồ nhân quả đơn thuần. Nó cũng xác định hàm phụ thuộc giữa các biến.

Lưu ý ta có thể thực hiện nhiều thao tác suy luận nhân quả, bao gồm việc tính toán độ lớn của các tác động nhân quả, chỉ thông qua biểu đồ mà không cần xác định các tham số cho mối quan hệ nhân quả.

*(1) Nhân quả trực tiếp*

Cách đơn giản nhất để mối tương quan giữa hai biến số phát sinh là khi một biến số là nguyên nhân trực tiếp của biến số kia. Quan hệ nhân quả xảy ra khi một biến thay đổi, các yếu tố khác không đổi, dẫn đến sự thay đổi trong biến thứ hai. Trong ví dụ về khả năng vỡ nợ, ta có thể tạo một biểu đồ hai nút với một trong các nút là quy mô doanh nghiệp (có giá trị 0 nếu là doanh nghiệp nhỏ, và ngược lại là 1) và nút còn lại là khả năng vỡ nợ cho biết liệu một doanh nghiệp có vỡ nợ hay không. Trong trường hợp này, chúng ta hy vọng một doanh nghiệp quy mô nhỏ làm tăng  khả năng vỡ nợ.

{% include figure image_path="/assets/images/aicausal/chap3/ac04-1.png"%}

Nhân quả trực tiếp làm phát sinh sự phụ thuộc giữa hai biến. Trong ví dụ này, biến quy mô doanh nghiệp có tác động nhân quả trực tiếp tới biến khả năng vỡ nợ. Thiết lập này gợi nhớ đến mô hình học máy có giám sát, trong đó chúng ta có một tập dữ liệu với các đặc tính X, và mục tiêu Y, để tìm hiểu mối quan hệ giữa chúng.

Tuy nhiên, trong học máy, chúng ta thường bắt đầu với tất cả các đặc tính có sẵn và chọn những đặc tính có nhiều thông tin nhất về mục tiêu. Trong trường hợp nhân quả, chỉ những đặc tính thực sự có tác động nhân quả lên mục tiêu mới được đưa vào biểu đồ như nguyên nhân trực tiếp. 

Trong phần tiếp theo, chúng ta sẽ thấy có những cấu trúc khác có thể dẫn đến quan hệ dự báo mang ý nghĩa thống kê giữa hai biến nhưng không trực tiếp bao hàm nhân quả. Cùng đón đọc phần tiếp để tìm hiểu thêm về hai cấu trúc nhân quả khác, cũng như cách biểu diễn Mô hình Cấu trúc nhân quả thông qua các biểu đồ với Python. 


*Bài viết có tham khảo thêm từ  https://www.investopedia.com/terms/s/spurious_correlation.asp
