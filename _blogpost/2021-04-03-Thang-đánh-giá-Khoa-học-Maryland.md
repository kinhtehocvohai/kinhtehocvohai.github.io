---
layout: single
title: Thang đánh giá Khoa học Maryland
excerpt: "Trong bài viết này chúng tôi sẽ giới thiệu với các bạn thang đánh giá độ mạnh của các phương pháp nghiên cứu khoa học"
toc: true
categories:
  - blog posts
tags:
  - suy luận nhân quả
permalink: /blogpost/marylandscale
---

Trong 4 tháng vừa qua Fanpage Kinh tế học vô hại đã chia sẻ loạt bài “Suy luận Nhân quả với Python” và giới thiệu nhiều “vũ khí” khoa học khác nhau giúp xác định quan hệ nguyên nhân – kết quả. Các “vũ khí” này rất hữu dụng và có thể sử dụng trong nhiều bối cảnh khác nhau như kinh tế, chính sách, giáo dục, tâm lý học, kinh doanh,… Chúng ta cũng đã thảo luận cách áp dụng và ưu, nhược điểm của mỗi phương pháp. 


Nhưng trước khi sử dụng các “vũ khí” này trong thực chiến, hẳn bạn cũng muốn biết tương quan sức mạnh của các vũ khí?


Trong bài viết này chúng tôi sẽ giới thiệu với các bạn thang đánh giá bằng chứng nhân quả của Trung tâm nghiên cứu chính sách tăng trưởng kinh tế địa phương (What works centre for local economic growth) thuộc London School of Economics and Political Science (LSE), Anh Quốc. Thang đo này dựa trên [Thang đánh giá khoa học Maryland (SMS)](https://whatworksgrowth.org/resources/the-scientific-maryland-scale/) và bao gồm 5 cấp độ tăng dần theo độ mạnh của phương pháp nghiên cứu như sau:


![image-center](/assets/images/blogpost/sms.png){: .align-center}

## Cấp độ 1: So sánh cắt ngang hoặc so sánh trước sau   

-    So sánh dữ liệu “cắt ngang” (crosssectional data) của nhóm can thiệp với nhóm đối chứng, hoặc,
-    So sánh nhóm can thiệp trước và sau khi có can thiệp  vắng mặt nhóm đối chứng
Cấp độ này không sử dụng các biến kiểm soát khi phân tích thống kê khác biệt giữa nhóm can thiệp và đối chứng hoặc khác biệt của cùng một đối tượng ở các thời điểm khác nhau.


## Cấp độ 2:  Sử dụng biến kiểm soát

Cấp độ 2 là phiên bản nâng cấp của cấp độ 1 nhưng có sử dụng các biến kiểm soát hợp lý nhằm loại bỏ các khác biệt “cắt ngang” giữa nhóm can thiệp với nhóm đối chứng hoặc thay đổi của các nhân tố vĩ mô trước và sau can thiệp


## Cấp độ 3: Hồi quy và ghép cặp

So sánh các kết quả của nhóm can thiệp trước và sau khi có can thiệp, cùng với nhóm chứng để cho ra kết quả giả tưởng trong trường hợp không có can thiệp, có sử dụng nhóm đối chứng (ví dụ như phương pháp sai khác của biến thiên). Đưa ra được lý do vì sao nhóm được chọn lại phù hợp làm nhóm đối chứng cho nhóm can thiệp và những bằng chứng thuyết phục để ủng hộ cho tính tương đồng giữa hai nhóm. Các phương pháp như hồi quy và ghép cặp điểm xu hướng có thể được dùng để ước lượng sự khác biệt giữa nhóm can thiệp và nhóm chứng. Tuy nhiên các phương pháp này nhiều khả năng bỏ  sót  các sai khác quan trọng mà ta không quan sát được. 


## Cấp độ 4: Sử dụng biến công cụ hoặc Thiết kế Nghiên cứu gián đoạn

Thực hiện can thiệp mô phỏng ngẫu nhiên (quasi-randomness) nhằm đảm bảo nhóm can thiệp và nhóm đối chứng chỉ khác biệt về mức độ tiếp xúc với can thiệp được thiết kế như thể ngẫu nhiên. Điều này thường được thực hiện thông qua việc sử dụng biến công cụ hoặc tính gián đoạn trong can thiệp. Cấp độ này cũng  đòi hỏi chứng minh và bảo vệ tính phù hợp của phương pháp sử dụng. 


## Cấp độ 5: Thử nghiệm Đối chứng Ngẫu nhiên

Dành cho các thiết kế nghiên cứu thực hiện chỉ định ngẫu nhiên nhóm can thiệp và nhóm đối chứng. Ví dụ điển hình nhất là Thử Nghiệm Đối Chứng Ngẫu Nhiên (RCT). Cần cung cấp đầy đủ bằng chứng cho thấy sự tương đồng giữa nhóm can thiệp và nhóm đối chứng, và không có sự khác biệt đáng kể về khởi điểm và xu hướng vận động giữa các nhóm này. Các biến kiểm soát có thể được sử dụng để khắc phục sự khác biệt giữa hai nhóm nói trên; tuy nhiên, việc bổ sung các biến này không được có tác động lớn đến kết quả chính. Cần phải chỉ ra rằng vấn đề từ bỏ can thiệp chọn lọc không nghiêm trọng và có thể bỏ qua. Cần hạn chế hoặc lý tưởng nhất là không để xảy ra hiện tượng tạp nhiễm can thiệp đối trong nhóm nhóm đối chứng.


**Hãy cùng tìm đọc thêm về chuỗi bài viết [“Suy luận Nhân quả với Python”](http://kinhtehocvohai.com/pythoncausal/) để hiểu rõ hơn về các phương pháp nhân quả.** 
{: .notice--warning}
