---
layout: single
sidebar:
 nav: aicausal
title: Phương hướng tương lai - Phần 1
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 19"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac19
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 19**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Suy luận nhân quả cung cấp một bộ khung khái niệm và kỹ thuật để giải quyết các câu hỏi về tác động của các hành động, can thiệp thực tế hoặc giả định. Một khi hiểu được tác động đó, chúng ta có thể lật ngược lại câu hỏi và truy  hành động nào nhiều khả năng dẫn đến một sự kiện cụ thể. Quy trình này cung cấp một “ngôn ngữ” chính thức để bàn về các mối quan hệ nhân quả. Tuy nhiên không phải mọi câu hỏi về nguyên nhân đều có lời giải đáp dễ dàng. Hơn nữa, việc tìm lời giải đáp hay thậm chí diễn giải và hiểu đúng ý nghĩa của nó cũng không phải là nhiệm vụ đơn giản. Đồ thị nhân quả đã được thảo luận trong những chương mở đầu cung cấp một phương thức thuận tiện để bàn về những vấn đề này, đồng thời cho phép suy luận về những mối quan hệ phụ thuộc về mặt thống kê trong dữ liệu quan sát.

Mô hình nhân quả cấu trúc (SCM) tiến thêm một bước gần hơn tới cách suy luận trực quan này bằng cách đưa ra các giả định chính thức về dạng tham số của các biến tương tác. Tuy nhiên việc xây dựng biểu đồ nhân quả và SCM có thể trở nên khó khăn khi số lượng các biến tăng lên. Một số hệ thống gần như không thể mô hình hoá được theo cách này. Lấy ví dụ, làm thế nào để vẽ được biểu đồ nhân quả cho các điểm ảnh, thậm chí chỉ trong một bức ảnh? Số lượng các tham số gần như vượt khỏi tầm kiểm soát. 

May mắn là không phải mọi vấn đề đều đòi hỏi toàn bộ biểu đồ nhân quả. Thông thường, chúng ta chỉ quan tâm đến mối quan hệ nhân quả liên quan tới một mục tiêu cụ thể. Đây là lúc phương pháp dựa trên bất biến (như IRM) bước vào “cuộc chơi” hướng tới việc cho phép mô hình học được các đặc tính ổn định qua nhiều môi trường (hay qua các quy trình tạo dữ liệu khác nhau). Mô hình này cho phép tổng quát hoá ngoài phân phối. Trái ngược với đồ thị nhân quả hoặc SCM khi mà cách duy nhất để xác thực các giả định về tương tác giữa các biến là thông qua thử nghiệm, IRM cho phép kiểm định trên một tập dữ liệu kiểm định chưa được quan sát. 

**Các cách tiếp cận tương đương**

Ngoài các phương pháp dựa trên bất biến, liệu có còn những cách khác để tiếp cận khái quát hoá ngoài phân phối? Nhìn chung, có hai nhánh tiếp cận chính: một là học để khớp với phân phối của các đặc tính (hoặc ước lượng biểu diễn dữ liệu), hai là sử dụng kỹ thuật tối ưu hoá.

**Thích ứng miền**

Kỹ thuật thích ứng miền (Domain Adaption) là một nhánh của Học chuyển giao (Transfer Learning). Trong đó, mô hình học một tác vụ trong miền gốc có chứa một số phân phối của đặc tính, và sau đó có khả năng thực hiện tốt cùng một nhiệm vụ ở miền mục tiêu có chứa phân phối của đặc tính khác với miền gốc. Các miền đóng vai trò giống như các môi trường trong các phương pháp tiếp cận dựa trên các biến, cụ thể, miền gốc là môi trường đã được huấn luyện, trong khi đó miền mục tiêu là bất kỳ môi trường nào chưa được huấn luyện.

Ở một khía cạnh nào đó, thích ứng miền cũng dựa trên bất biến – nó tìm kiếm một dạng biểu diễn chung có phân phối tương tự nhau trên cả miền nguồn và miền mục tiêu (cũng giống như qua các môi trường). Tuy nhiên, các tính năng nhân quả bất biến không nhất thiết phải tuân theo cùng một phân phối qua các môi trường khác nhau. Ví dụ, một con bò trên tuyết sẽ không tạo ra phân bố điểm ảnh giống hệt với một con bò trên cát, và những đặc tính nhân quả đại diện cho loài bò.

**Học chuẩn mạnh**

Ý tưởng học qua nhiều môi trường không phải mới mẻ đối với các phương pháp tiếp cận dựa trên bất biến. Học chuẩn mạnh có giám sát (Robust Supervised Learning) là một nhánh bao gồm các kỹ thuật ra đời từ trước và sử dụng thiếp lập đa môi trường như IRM, với mục tiêu tương tự là cho phép hoặc tăng cường tổng quát hóa ngoài phân phối. Nói một cách khác, mục tiêu đặt ra là mô hình dự báo chuẩn mạnh đối với sự thay đổi trong phân bố của các yếu tố đầu vào.

So với IRM, sự khác biệt nằm ở hàm tổn thất. Ý tưởng chính là thêm các đại lượng cơ sở cụ thể vào hàm tổn thất, và cố gắng điều chỉnh các đại lượng này sao cho nhiễu trong các môi trường có tổn thất cao không chiếm ưu thế. Sau đó, giảm thiểu tối đa tổn thất sẽ đảm bảo mô hình hoạt động tốt trên mọi môi trường đã biết. Hơn nữa, một mô hình dự báo chuẩn mạnh sẽ hoạt động tốt trong các môi trường mới được nội suy từ những môi trường đã qua huấn luyện. Điều này sẽ làm cải thiện khả năng tổng quát hoá ngoài phân phối, nhưng không cho phép ngoại suy ngoài môi trường đã được quan sát trong tập huấn luyện, trong khi IRM có thể ngoại suy dựa vào dự đoán bất biến. 

**Học tổng hợp**

Các cách tiếp cận như Thích ứng miền, Học chuẩn mạnh, hay nói chung hơn là Học chuyển giao đều cố gắng giải quyết vấn đề tổng quát hoá ngoài phân phối ở một mức độ nhất định. Thật không may, việc học các đặc tính bất biến với các phân phối khác nhau qua nhiều môi trường vẫn còn là thách thức. Những cách tiếp cận này tốt trong việc nội suy, không phải ngoại suy.

Đây là lúc các phương pháp tiếp cận Học tổng hợp (Meta-learning) như mô hình học tổng hợp bất khả tri (MAML) phát huy tác dụng. Ý tưởng cơ bản là học các tác vụ với một số lượng nhỏ các mẫu đã được gắn mác. Huấn luyện mô hình học tổng hợp được chia ra làm hai bước bao gồm học và huấn luyện. Mục tiêu của mô hình học là nhanh chóng học các tác vụ mới từ một số lượng nhỏ dữ liệu, do đó nó còn được gọi là học nhanh. Tác vụ ở đây có thể là bất kỳ bài toán học có giám sát nào. Mô hình học này được huấn luyện bởi học tổng hợp để có thể học được nhiều nhiệm vụ khác nhau. Học tổng hợp thực hiện nhiệm vụ này bằng cách cho mô hình học thấy hàng trăm, hàng nghìn tác vụ khác nhau.

Việc học sau đó diễn ra ở hai cấp độ. Cấp độ thứ nhất là tập trung vào việc  thu thập nhanh kiến thức của mỗi tác vụ thông qua một vài mẫu dữ liệu. Cấp độ thứ hai là thu lượm và tổng hợp các thông tin từ tất cả các tác vụ. Trong trường hợp MAML (phương pháp dựa trên tối ưu hoá), mô hình học (cấp độ đầu tiên) có thể học nhanh tối ưu trên tác vụ mới chỉ qua một vài bước điều chỉnh độ dốc bởi học tổng hợp có khả năng khởi tạo tham số cho mô hình tốt. Cách tiếp cận này gần với bài toán học mô hình phân loại tối ưu qua nhiều môi trường, và có thể được khai thác thêm để học các đặc tính bất biến trong dữ liệu. Đã có nhiều bài báo nghiên cứu kết hợp giữa nhân quả và học tổng hợp. 


