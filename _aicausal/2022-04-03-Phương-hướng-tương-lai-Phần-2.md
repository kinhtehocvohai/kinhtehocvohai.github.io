---
layout: single
sidebar:
 nav: aicausal
title: Phương hướng tương lai - Phần 2
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 20"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac20
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 20**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Trong phần này, chúng ta cùng trao đổi về tương lai của các phương pháp nhân quả nói chung, và các phương pháp dựa trên bất biến nói riêng.

**Học tăng cường nhân quả**

Học tăng cường (Reinforcement learning) là lĩnh vực nghiên cứu cách đưa ra quyết định hành động  của một chủ thể nhằm tối đa hoá lợi ích tương lai trong một môi trường có tính tương tác và không chắc chắn. Các chủ thể này dựa vào nhiều mô phỏng (và đôi khi là dữ liệu thực) để tìm hiểu hành động nào dẫn tới phần thưởng lớn trong một hoàn cảnh cụ thể. Mặt khác, nhân quả đồng thời hướng tới việc tính toán tác động của hành động, và cho phép áp dụng  những hiểu biết đó trong những tình huống mới. Hai lĩnh vực này đã phát triển một cách độc lập và hầu như không có tương tác, cho đến thời gian gần đây. Sự kết hợp giữa hai lĩnh vực này có thể tạo nên một lĩnh vực nghiên cứu hiệu quả, đồng thời mở rộng phạm vi của cả quan hệ nhân quả và học tăng cường.

Giữa khái niệm can thiệp trong suy luận nhân quả và các hành động được thực hiện trong học tăng cường có một mối liên hệ tự nhiên. Trong mỗi giai đoạn (một chu trình vận hành của hệ thống, ví dụ như một ván cờ vua hay cờ vây) của học tăng cường, chủ thể thực hiện các hành động. Điều này xác định một mô hình tạo lập dữ liệu cho phần thưởng mà chủ thể quan tâm và các chuỗi hành động khác nhau sẽ tạo ra các phần thưởng khác nhau. Bởi chủ thể có thể đưa ra các lựa chọn hành động, mỗi hành động sẽ trở thành một can thiệp vào mô hình tạo lập dữ liêu. Khi đó, chúng ta có thể vận dụng suy luận nhân quả. Ví dụ, trong cấp độ thứ ba của bậc thang nhân quả, tư duy phản thực có thể được áp dụng để lập luận về những hành động chưa xảy ra. Việc sử dụng kỹ thuật nhân quả có thể làm giảm số lượng các trường hợp mà chủ thể cần xem xét, hoặc giúp giải thích các yếu tố gây nhiễu.

Về nguyên tắc, các phương pháp dựa trên bất biến như IRM học cách xác định các bất biến từ nhiều môi trường. Đặc điểm này có thể được vận dụng trong học tăng cường. Mỗi vòng học tăng cường bao gồm tất cả các trạng thái nằm giữa trạng thái đầu và cuối. Bởi các vòng học độc lập với nhau, theo thuật ngữ của phương pháp dựa trên bất biến như IRM (Giảm thiểu rủi ro bất biến), chúng có thể được xem như các môi trường khác nhau. Sau đó, chủ thể có thể học được những quy tắc hiệu quả để sử dụng phần bất biến của hành động làm tăng phần thưởng.

Tuy việc ứng dụng học tăng cường cho ứng dụng thương mại vẫn còn ở giai đoạn sơ khai, việc kết hợp học tăng cường với quan hệ nhân quả có tiềm năng lớn.  Trước đó, chúng ta cần giải quyết một số câu hỏi. Ví dụ, làm thế nào để kết hợp tính trừu tượng  khi lập trình mô hình nhân quả với học tăng cường để giúp tìm ra các quyết định tốt nhất? Công cụ và thư viện nào cần thiết để kích hoạt các ứng dụng thương mại trong trường hợp này?

**IRM và môi trường**

IRM sử dụng ý tưởng huấn luyện trong nhiều môi trường để thu được khả năng tổng quát hoá ngoài phân phối. Tuy nhiên, rất ít bộ dữ liệu đi kèm với chú thích sẵn có. Có ít nhất hai cách để giải quyết vấn đề này.

Đầu tiên là lưu ý đến môi trường khi thu thập dữ liệu, và thu thập siêu dữ liệu (dữ liệu về dữ liệu). Việc này có thể thực hiện dễ dàng (ví dụ: thu thập vị trí địa lý của hình ảnh trong phần cài đặt nếu có thể, không vi phạm quyền riêng tư của người dùng), hoặc cực kỳ khó khăn (đòi hỏi gắn nhãn thủ công sau thu thập).

Một hướng giải quyết khác hấp dẫn nhưng chưa được thử nghiệm rộng rãi là kết hợp IRM với phân tích cụm (clustering) để phân loại một tập dữ liệu duy nhất theo các môi trường. Câu hỏi đặt ra là làm thế nào để phân cụm theo cách xác định được các môi trường đa dạng và có ý nghĩa. Bởi cách tiếp cận phân tích cụm hiện tại đơn thuần là tương quan, vì vậy có thể bị ảnh hưởng bởi tương quan giả. Điều này đặt ra nhiều thách thức.

Nghiên cứu tác động của việc lựa chọn môi trường và cách tạo ra hoặc sắp xếp các bộ dữ liệu theo nhiều môi trường sẽ là đóng góp có giá trị để làm cho các phương pháp dựa trên bất biến được áp dụng rộng rãi.

**Suy luận nhân quả cho tính công bằng của thuật toán**

Phần Vấn đề đạo đức trong học máy đã thảo luận một số khái niệm về tính công bằng trong các bài toán dự báo và các công cụ nhân quả có thể giải quyết các bài toán này. Chúng chuyển từ phương pháp tiếp cận truyền thống hoàn toàn lệ thuộc vào dữ liệu sang hướng nhấn mạnh sự cần thiết của việc thêm vào kiến thức bổ sung về cấu trúc của thế giới dưới dạng mô hình nhân quả. Những kiến thức này đặc biệt có giá trị vì nó cho ta biết những thay đổi trong các biến truyền đi như thế nào trong hệ thống (có thể là tự nhiên, kỹ thuật, hay xã hội). Các giả định nhân quả rõ ràng loại bỏ sự mơ hồ khỏi các phương pháp chỉ phụ thuộc vào các mối tương quan thống kê. Việc loại bỏ phân biệt đối xử thông qua lý luận nhân quả cũng là một lĩnh vực nghiên cứu sôi động. Việc những nỗ lực nhằm thúc đẩy tính minh bạch và công bằng trong các hệ thống học máy ngày càng phát triển sẽ tạo đà cho lý luận nhân quả tiếp tục hướng các thuật toán hướng tới sự công bằng. 
