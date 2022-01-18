---
layout: single
title: Lỗi Excel và đánh giá hiệu quả truy vết Covid ở Anh
excerpt: "Excel và lỗi quản lý dữ liệu đã tạo ra một cơ hội vô tiền khoáng hậu cho các nhà nghiên cứu thử nghiệm tự nhiên."
toc: false
categories:
  - blog posts
tags:
  - khoa học dữ liệu
permalink: /blogpost/covid-tracing-england
---

Nước Anh (England) đã tiêu tốn khoảng 12 tỷ bảng (khoảng 360 ngàn tỷ đồng) cho hệ thống truy vết Covid. Nhân viên truy vết, với sự hỗ trợ của công nghệ, thu thập thông tin từ những người mới xét nghiệm dương tính Covid và báo cho những người tiếp xúc gần tự cách ly. Trên lý thuyết đây là phương pháp quan trọng để ngành y tế cộng đồng kiểm soát các bệnh truyền nhiễm.

Câu hỏi đặt ra là biện pháp tốn kém như thế có đáng làm hay không? Nhân viên truy vết thường được tuyển dụng gấp và không kịp đào tạo kĩ lưỡng. Những người mắc Covid không phải lúc nào cũng hợp tác, thậm chí chống đối. Nhiều người không muốn chia sẻ thông tin đời tư, không tin vào chính quyền, hoặc lo ngại lừa đảo và các vấn nạn an ninh mạng khác. Một báo cáo chính thức đăng trên website chính phủ  tháng 9/2020 cho rằng hiệu quả truy vết ở Anh rất thấp vì ít người sử dụng các phương tiện truy vết và nhiều người không tuân thủ tự cách ly khi được yêu cầu.


Hãy tưởng tượng một thử nghiệm lý tưởng. Các nhà nghiên cứu ngẫu nhiên chia các tình nguyện viên thành 2 nhóm và đưa họ tới 2 hoang đảo giống hệt nhau đủ điều kiện để con người sinh sống. Khác biệt duy nhất là một hoang đảo có hệ thống truy vết và hoang đảo còn lại thì không. Sau đó các nhà nghiên cứu đưa mầm bệnh Covid vào 2  hoang đảo cùng một lúc. Một thời gian sau, so sánh hai quần thể người này (tỉ lệ người nhiễm, tỉ lệ tử vong), họ sẽ thu được câu trả lời khả tín về hiệu quả của truy vết.

Tất nhiên một thử nghiệm như thế đã không diễn ra (thật may mắn, đấy không phải là cách người ta đang làm khoa học). Trong khi đó các thử nghiệm trên khỉ hay chuột bạch cũng chẳng thể giúp ích vì chúng không có hành vi xã hội phức tạp như con người. Các nghiên cứu ban đầu dựa trên dữ liệu quan sát được giữa các nhóm người ở các khu vực địa lý khác nhau. Tuy nhiên các nhà nghiên cứu khó có thể đảm bảo quan sát được toàn bộ các yếu tố chi phối đồng thời việc vận hành hệ thống truy vết và diễn biến dịch Covid từ các dữ liệu này.

Excel và lỗi quản lý dữ liệu đã tạo ra một cơ hội vô tiền khoáng hậu cho các nhà nghiên cứu thử nghiệm tự nhiên.

Với nhiều người Excel là công cụ không thể thiếu trong công việc. Ngày nay chúng ta thường dùng các file .xlsx nhưng phiên bản cũ .xls không quá xa lạ với nhiều người. Và bạn có biết file .xls không thể lưu giữ nhiều hơn 65,536 dòng.

Điều bất ngờ là hệ thống truy vết trị giá nhiều tỉ bảng Anh lại sử dụng định dạng file .xls cũ kĩ để xử lý lượng dữ liệu lớn. Tháng 10/2020, khi số ca dương tính mới vượt ngưỡng giới hạn 65,536, 15,841 bệnh nhân đã bị file .xls tự động gạt bỏ không đưa vào hệ thống. Hậu quả là nhiều người tiếp xúc gần không được nhận thông báo tự cách ly kịp thời.

"Lỗi hệ thống" tạo ra số lượng lớn các ca chậm cách li rải rác khắp nước Anh và sự phân tán theo địa lý của lỗi này khá ngẫu nhiên, như thể "tự nhiên" đã tạo ra một thử nghiệm để con người đánh giá hiệu quả truy vết. Ví dụ quận Adur và Watford giống nhau đến 98% dựa trên bộ chỉ số diễn tiến dịch và đặc điểm dân cư xã hội ngay trước khi có lỗi Excel. Tuy nhiên tính trung bình trên 1,000 người lỗi Excel làm chậm truy vết 6.3 ca ở Adur và chỉ 3.44 ca ở Watford, một sự khác biệt khá lớn.

![image-center](/assets/images/blogpost/covid_tracing.png){: .align-center}

Mô hình kinh tế lượng chỉ ra rằng các địa phương bị ảnh hưởng nhiều từ "lỗi hệ thống" này có tỉ lệ ca mắc và tử vong vì Covid tăng vọt. (Lưu ý là các nhà khoa học đã cố gắng kiểm soát khác biệt giữa các địa phương thời điểm trước khi có lỗi Excel). Từ đó họ ước lượng rằng trong 6 tuần, cứ mỗi ca Covid chậm truy vết làm phát sinh 25 ca Covid và 0.33 ca tử vong. Các mô hình với giả định khác nhau ước lượng việc kịp thời truy vết lẽ ra đã có thể làm giảm khoảng 126,836 - 185,188 ca bệnh và 1,521- 2,049 ca tử vong trên toàn nước Anh nếu không có lỗi Excel.

Đây là một thử nghiệm tự nhiên “bất đắc dĩ” đã được tiến hành để đánh giá hiệu quả của hệ thống truy vết ở Anh. Có thể nói “lỗi Excel” ở đây đã đóng vai trò một chỉ định can thiệp  “như thể” ngẫu nhiên thông qua danh sách những người “tình cờ” bị gạt bỏ khỏi file .xls. Kết quả phân tích kinh tế lượng cho thấy, trái với nhiều nghi ngờ về tính hiệu quả của hệ thống truy vết, phương pháp này vẫn đóng một vai trò quan trọng trong việc giảm thiểu một lượng lớn các ca bệnh và tử vong do Covid. 

Lời cảnh báo cuối cùng, hãy thận trọng với Excel khi xử lý và xây dựng hệ thống dữ liệu lớn. Và nếu hợp tác và tuân thủ các yêu cầu của các cơ quan truy vết, bạn đang giúp ích rất nhiều cho cộng đồng trước đe dọa của Covid.


*Bài viết này dựa trên nghiên cứu “Truy vết có hiệu quả? Bằng chứng bán thử nghiệm từ lỗi Excel ở Anh” của tác giả Thiemo Fetzer và Thomas Graeber (2020), công bố tại Chuỗi Nghiên cứu Thảo luận của Trung tâm Nghiên cứu Chính sách Kinh tế (CEPR). Một phiên bản khác của nghiên cứu này được đăng trên tạp chí PNAS (2021)




