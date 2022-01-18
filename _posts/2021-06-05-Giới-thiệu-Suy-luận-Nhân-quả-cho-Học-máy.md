---
layout: single
sidebar:
 nav: aicausal
title: Giới thiệu Suy luận Nhân quả cho Học máy
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 1"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/intro
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 1**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Không thể phủ nhận Học máy (Machine Learning) trong những năm gần đây đã đạt được những tiến bộ vượt bậc.Nó cho phép tìm kiếm hình ảnh theo nội dung, dịch ngôn ngữ tự động, cũng như tổng hợp và tạo lập hình ảnh, giọng nói, video. Đồng thời, Học máy cũng được ứng dụng rộng rãi trong các doanh nghiệp, bao gồm việc giải quyết các nhiệm vụ dự báo như dự đoán tỷ lệ khách hàng ngừng sử dụng sản phẩm, khả năng vỡ nợ, khả năng hỏng hóc của các thiết bị sản xuất, v.v.

 ![image-center](/assets/images/aicausal/chap1/intro.png){: .align-center}

Những kết quả phi thường của việc ứng dụng học máy là nhờ vào việc học có giám sát trên tập dữ liệu huấn luyện lớn (kết hợp với sức mạnh tính toán). Có thể nói thế mạnh vượt trội của mô hình học máy có giám sát là khả năng dự báo. Khi mục tiêu là dự báo một kết quả có thể xảy ra, và có nhiều khả năng của kết quả đó có thể phát sinh cũng như các đặc tính liên quan đến chúng, chúng ta có thể sử dụng mô hình học có giám sát. Khi học máy đã trở nên phổ biến, phạm vi ảnh hưởng của nó trong các quy trình kinh doanh không chỉ gói gọn trong việc dự báo đơn thuần, mà còn tác động tới quá trình đưa ra quyết định. 

Tuy nhiên, có những giới hạn cơ bản với việc suy luận chỉ dựa trên kết quả dự báo. Ví dụ, điều gì sẽ xảy ra nếu ngân hàng tăng hạn mức tín dụng khách hàng? Những câu hỏi này không thể được trả lời bằng một mô hình tương quan được xây dựng trên dữ liệu đã quan sát trước đó, bởi chúng liên quan đến sự thay đổi tiềm năng trong hành vi của khách hàng theo sự thay đổi hạn mức tín dụng. Trong nhiều trường hợp, kết quả của một quá trình ra quyết định lại là sự can thiệp – một hành động  nhằm thay đổi một đối tượng khác trong thế giới. 

Chuỗi bài sắp tới sẽ cung cấp thông tin cũng như củng cố lập luận rằng các mô hình học máy dự báo tương quan thuần tuý không được trang bị để đưa ra suy luận trong trường hợp có những can thiệp như vậy, do đó dễ dẫn đến thiên lệch. Để đưa ra những quyết định dựa trên dữ liệu có can thiệp, chúng ta cần hiểu về quan hệ nhân quả.

Ngay cả đối với các mô hình dự báo thuần tuý, vốn là  điểm mạnh của các mô hình học máy có giám sát, việc áp dụng tư duy nhân quả cũng rất có lợi. Theo định nghĩa, các mối quan hệ nhân quả là bất biến, nghĩa là chúng không thay đổi trong các hoàn cảnh và môi trường khác nhau. Đây là một đặc tính rất đáng kỳ vọng cho các mô hình học máy thường được dùng để dự đoán trên dữ liệu mới nằm ngoài quá trình huấn luyện. Sự giao thoa giữa suy luận nhân quả và học máy là một lĩnh vực nghiên cứu đang mở rộng nhanh chóng, giúp chúng ta xây dựng các hệ thống học máy mạnh, đáng tin cậy và bớt thiên lệch hơn. 

Chuỗi bài “SUY LUẬN NHÂN QUẢ CHO HỌC MÁY” sẽ cung cấp những kiến thức nền tảng cơ bản về suy luận nhân quả trong bối cảnh của khoa học dữ liệu và học máy. Các biểu đồ nhân quả sẽ được giới thiệu với mục tiêu loại bỏ các rào cản về lý thuyết. Những kiến thức nền tảng này sẽ được sử dụng để khám phá những ý tưởng xoay quanh dự báo bất biến, điều này cho thấy một số lợi ích của đồ thị nhân quả cho các vấn đề dữ liệu nhiều chiều. Ngoài ra, ngay cả các bài toán học máy cổ điển (như phân loại hình ảnh) cũng được chứng minh có thể hưởng lợi như thế nào từ các công cụ suy luận nhân quả.



