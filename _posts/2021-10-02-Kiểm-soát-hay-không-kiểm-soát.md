---
layout: single
title: Kiểm soát hay không kiểm soát
excerpt: "Biến kiểm soát là một phương tiện quan trọng để loại bỏ tác động của nhiễu và cho kết quả đáng tin cậy hơn; tuy nhiên, liệu điều này có nghĩa là ta cố kiểm soát càng nhiều yếu tố càng tốt?"
toc: false
categories:
  - blog posts
tags:
  - quan he nhan qua
  - causality
permalink: /blogpost/controlvariable
---

Dữ liệu thử nghiệm là vật liệu lý tưởng để tiến hành suy luận nhân quả. Tuy nhiên các thử nghiệm ngẫu nhiên không sẵn có và trong nhiều hoàn cảnh khó thu thập.

Khi sử dụng dữ liệu quan sát để suy luận nhân quả, Biến Kiểm soát là một phương tiện quan trọng giúp loại bỏ tác động của nhiễu (các nhân tố khác tác động lên cả nguyên nhân và kết quả ta muốn nghiên cứu).

Nếu làm tốt việc này, dữ liệu quan sát sẽ gần giống với dữ liệu thử nghiệm và cho kết luận đáng tin cậy hơn về quan hệ nhân quả. 

Ví dụ khi muốn đánh giá tác động của học vấn lên thu nhập, ta muốn loại bỏ tác động của năng lực bẩm sinh. Những người thông minh thiên bẩm dễ thành công trong cả học vấn và kiếm tiền.

Khi đánh hiệu quả hỗ trợ hồi phục của một loại thuốc, ta muốn kiểm soát mức độ bệnh lý. Nếu chỉ người bị bệnh nặng mới được dùng thuốc thì kết quả quan sát được khi không kiểm soát sẽ đánh giá quá thấp hiệu quả của thuốc. Hãy tham khảo hình động sau để thấy được tác động của biến can thiệp


![image-center](/assets/images/animatedcausality/ac01/IV.gif){: .align-center}

**Tuy nhiên điều này không có nghĩa là ta cố kiểm soát càng nhiều yếu tố càng tốt.**

Ta không nên kiểm soát kết quả chung khi đánh giá quan hệ nhân quả của hai biến. Không nên kiểm soát kết quả tuyển dụng lập trình viên khi xem xét quan hệ giữa kĩ năng giao tiếp và khả năng lập trình.
Những người giao tiếp không tốt chỉ trúng tuyển khi rất giỏi chuyên môn lập trình. Đây không phải bằng chứng để  kết luận việc học lập trình làm giảm khả năng giao tiếp của con người.

![image-center](/assets/images/animatedcausality/ac07/IV.gif){: .align-center}


Ta cũng không nên kiểm soát biến sau khi can thiệp đã diễn ra. Khi đánh giá tác động của thuế tiêu thụ thuốc lá lên sức khỏe của dân cư, ta không muốn kiểm soát lượng thuốc tiêu thụ. Khó có thể quan sát tác động cải thiện sức khỏe dân cư của việc đánh thuế làm tăng giá thuốc, nếu ta cố định không cho lượng tiêu thụ thuốc lá thay đổi.

![image-center](/assets/images/animatedcausality/ac08/IV.gif){: .align-center}

