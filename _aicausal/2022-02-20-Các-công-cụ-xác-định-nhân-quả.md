---
layout: single
sidebar:
 nav: aicausal
title: Các công cụ xác định nhân quả
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 17"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac17
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 17**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Các phương pháp tiếp cận nhân quả dựa trên các đặc tính hay các mối tương quan bất biến mà chúng ta đã trao đổi không đòi hỏi các công cụ chuyên dụng. Dự đoán nhân quả bất biến (ICP) và Giảm thiểu rủi ro bất biến (IRM) đều có thể được thực hiện bởi các công cụ chung trong lĩnh vực học máy.

Tuy vậy, các tác giả của bài báo về ICP cũng cung cấp các thư viện (package) tương ứng trong ngôn ngữ lập trình R có tên: InvariantCausalPrediction và nonlinearICP. Các thư viện này giúp việc áp dụng các phương pháp trở nên dễ dàng hơn, và hơn thế cung cấp một số tiện ích bổ trợ như vẽ đồ thị chuyên dùng để biểu diễn khoảng tin cậy của hệ số nhân quả. Hiện chúng tôi chưa tìm thấy một phần mềm tương tự cho IRM, nhưng các tác giả có cung cấp nguồn lưu trữ code để tái lập kết quả của bài báo.

Trong bài này, chúng ta hãy cùng liệt kê một số dự án mã nguồn mở hỗ trợ suy luận nhân quả dựa trên mô hình nhân quả cấu trúc truyền thống

{% include figure image_path="/assets/images/aicausal/chap5/chap5_17_1.png" %} 

**DoWhy**

Microsoft Research đang phát triển thư viện DoWhy trên Python cho suy luận nhân quả kết hợp các yếu tố của mô hình nhân quả cấu trúc và kết quả tiềm năng. Thư viện được phát triển định hướng theo DataFrames nên dễ dàng phù hợp với quy trình phân tích dữ liệu trên Python. Đặc biệt DoWhy tách biệt rõ bốn giai đoạn của suy luận nhân quả.

Mô hình hoá: xác định biểu đồ nhân quả, hoặc các giả định cần thiết cho phương pháp tiếp cận kết quả tiềm năng (các nguyên nhân chung của can thiệp và biến kết quả).

Nhận diện: xác định biểu thức cần thiết để đánh giá dựa trên phân bố xác suất có điều kiện.

Ước lượng: ước lượng hiệu quả can thiệp. Có nhiều phương pháp ước lượng có sẵn trong DoWhy bao gồm cả phương pháp dựa trên học máy từ một thư viện nhân quả khác của Microsoft có tên là EconML.

Phản bác: đánh giá mức độ chắc chắn của kết luận. Vì suy luận nhân quả phụ thuộc vào các giả định mô hình hoá, nên việc kiểm định các kết luận là rất quan trọng. DoWhy cung cấp một số phương pháp để làm điều này, có thể kể đến như đưa vào một biến giả nguyên nhân chunghay thay thế can thiệp (điều trị) bằng giả dược ngẫu nhiên.

Ngoài những điều kể trên, DoWhy còn bao gồm một thuật toán mới có tên là “do-sampler”. Phần lớn suy luận nhân quả thường quan tâm đến một con số, ví dụ như sự khác biệt của biến kết quả khi một biến can thiệp nhị phân được áp dụng  (“tác động nhân quả trung bình của việc hút thuốc lá đối với tỷ lệ mắc bệnh ung thư là bao nhiêu?”). “do-sampler” được mở rộng trực tiếp từ giao diện lập trình ứng dụng pandas DataFrame, và không chỉ dùng để tính toán các tác động nhân quả để cho phép lấy mẫu từ phân phối can thiệp tổng thể. Hơn thế, nó còn có thể tính toán các số liệu thống kê của can thiệp. “do-sampler” rất có tiềm năng trong việc giúp suy luận nhân quả tới gần hơn với các nhà khoa học dữ liệu. 

**CausalDiscoveryToolbox**

CausalDiscoveryToolbox cung cấp cách triển khai của nhiều thuật toán được thiết kế để khám phá nhân quả - nỗ lực khôi phục toàn bộ biểu đồ nhân quả chỉ từ dữ liệu quan sát. Nó bao gồm nhiều phương pháp tiếp cận để xác định nhân quả và là một thư viện tương đối toàn diện, bao gồm các thuật toán để xác định nhân quả theo cặp (dùng để suy ra hướng nhân quả giữa hai biến), tạo khung đồ thị (tạo một biểu đồ vô hướng về các mối quan hệ nhân quả tiềm ẩn) và xác định đầy đủ mô hình biểu đồ nhân quả.

Tuy nhiên, hiện vẫn còn quá sớm để tin vào những kết luận về việc khám phá ra một cấu trúc nhân quả hoàn chỉnh của một vấn đề chỉ dựa vào dữ liệu quan sát. 

**CausalNex**

CausalNex là bộ công cụ được phát hành bởi QuantumBlack để giúp các nhà khoa học dữ liệu lập luận nhân quả. Nó cung cấp cả yếu tố có thể học cấu trúc biểu đồ để giúp xây dựng biểu đồ nhân quả và các công cụ để phù hợp với đồ thị đó như một mạng Bayes.

Yếu tố học cấu trúc được phát triển bởi DAGs và NOTEARS, và là một thuật toán sử dụng việc học cấu trúc biểu đồ như một bài toán tối ưu hoá liên tục. Ở dạng cơ bản nhất, nó giả định các mối quan hệ giữa các biến là tuyến tính (tuy nhiên khác với một số phương pháp xác định nhân quả, nó không giả định nhiễu Gaussian). Hơn nữa, thuật toán giả định rằng tất cả các biến đều được quan sát (tức là tồn tại dữ liệu cho tất cả các biến). Đáng tiếc là điều này thường ít khi xảy ra trong các vấn đề nhân quả.

Nếu thoả mãn được các giả định trên, thuật toán hoạt động tốt và cho phép người dùng đặt ra những điều kiện ràng buộc nghiêm ngặt (ví dụ như “các biến này không thể là nút con” hoặc “không có mối quan hệ nhân quả giữa hai biến này”). Điều này tạo ra điều kiện thuận lợi cho việc mã hoá trực tiếp kiến thức chuyên môn vào biểu đồ và sử dụng yếu tố học cấu trúc như một công cụ trợ giúp khi mà các mối quan hệ nhân quả vẫn còn là ẩn số. 

**Pyro**

Thư viện lập trình xác suất Pyro chủ yếu dành cho việc áp dụng các mô hình xác suất sâu và khớp chúng với suy luận biến thiên. Tuy nhiên, ngoài các công cụ dựa vào dữ liệu quan sát, thư viện có lệnh “do” để buộc một biến có một phân phối nhất định. Điều này cho phép mô phỏng từ phân phối can thiệp, miễn là đã biết mô hình nhân quả cấu trúc (và cả các phương trình). Sự giao thoa của lập trình xác suất với suy luận nhân quả tuy con non trẻ nhưng đầy hứa hẹn!

