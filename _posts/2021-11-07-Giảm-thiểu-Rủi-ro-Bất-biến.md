---
layout: single
sidebar:
 nav: aicausal
title: Giảm thiểu Rủi ro Bất biến
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 12"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac12
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 12**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Khi sử dụng dự đoán nhân quả bất biến (Invariant Causal Prediction-ICP), ta né tránh việc thiết lập mô hình cấu trúc nhân quả tổng thể, hay biểu đồ mô tả toàn bộ hệ thống đang được mô hình hoá. Tuy nhiên, chúng ta vẫn phải nghĩ về vấn đề này. 

Trong nhiều trường hợp, ngay cả việc thiết lập một biểu đồ nhân quả không hề đơn giản. Ví dụ, trong khi các mô hình cấu trúc nhân quả cung cấp một bộ khung lý thuyết hoàn chỉnh cho suy luận nhân quả, việc mã hoá các định luật vật lý đã biết thường không dễ dàng (ví dụ như định luật vạn vật hấp dẫn của Newton, hay định luật khí lý tưởng) dưới dạng biểu đồ nhân quả. Hay trong bài toán quen thuộc Nhận diện hình ảnh trong học máy, làm thế nào để mô hình hoá mối quan hệ nhân quả giữa từng điểm ảnh (pixel) và mục tiêu được dự đoán? Đây là một trong những câu hỏi gợi mở bài báo nghiên cứu [“Giảm thiểu rủi ro bất biến” (Invariant Risk Minimization-IRM)](https://arxiv.org/abs/1907.02893).

Giống như ICP, IRM sử dụng ý tưởng  huấn luyện trong nhiều môi trường. Tuy nhiên, khác với ICP, IRM không quan tâm đến việc xác định các nút cha mẹ của mục tiêu trong biểu đồ nhân quả. Thay vào đó, IRM tập trung vào tổng quát hoá ngoài bên ngoài phân phối được huấn luyện: hiệu năng của mô hình dự đoán  trong một môi trường mới. Kỹ thuật được đề xuất nhằm mục đích tạo ra một dạng biểu diễn dữ liệu mà một mô hình phân loại hay hồi quy có thể hoạt động tối ưu trong mọi môi trường. Các tác giả của IRM đã mô tả nguyên tắc này:

“Để tìm hiểu sự bất biến giữa các môi trường, hãy tìm một dạng biểu diễn dữ liệu sao cho mô hình phân loại tối ưu nhất của dạng dữ liệu đó phù hợp với mọi môi trường.”

Nói cách khác, ý tưởng cơ bản là tồn tại một cấu trúc nhân quả tiềm ẩn đằng sau vấn đề đang được nghiên cứu, và nhiệm vụ của chúng ta là khôi phục một dạng dữ liệu mã hoá phần của cấu trúc tác động đến mục tiêu nghiên cứu. Việc này khác với việc chọn các tính năng như trong ICP. Cụ thể, nó kết nối các đặc tính bậc thấp (như các điểm ảnh riêng lẻ) tới các dạng biểu diễn mã hoá các khái niệm cấp cao (ví dụ con bò trong nhận diện hình ảnh). 

**Hướng nhân quả** 
Ý tưởng về một hệ thống nhân quả tiềm ẩn tạo ra các đặc tính quan sát được đặc biệt hữu ích trong các bài toán về thị giác máy tính. Các nhà nghiên cứu từ lâu đã tìm hiểu quá trình khái quát hoá liên quan đến việc chuyển đổi từ các đối tượng trong thế giới thực sang dạng điểm ảnh. 


{% include figure image_path="/assets/images/aicausal/chap3/chap3_12_1.png" caption="Khi các đặc tính là nguyên nhân của mục tiêu, chúng ta đang “học” thuận chiều nhân quả. Khi đặc tính là các tác động, chúng ta đang “học” nghịch chiều nhân quả.  
" %}

Ví dụ, trong tự nhiên, bò có thể xuất hiện ở trên cánh đồng hay thậm chí trên bãi biển, hiểu một cách ngắn gọn thì có sự khác biệt giữa bò và khung cành mặt đất. Một mô hình mạng thần kinh nhân tạo (neural network) cố gắng dự đoán sự hiện diện của một con bò trong tập dữ liệu hình ảnh có thể được coi là một ví dụ của cách học theo hướng nghịch chiều nhân quả, bởi hướng của nhân quả ngược lại với hướng dự đoán. Cụ thể, sự hiện diện của một con bò trong hình ảnh gây ra một số dạng điểm ảnh nhất định, nhưng điểm ảnh  lại là dữ liệu đầu vào của mô hình và sự hiện diện của bò là kết quả đầu ra.

Cần chú ý rằng tập dữ liệu để huấn luyện mạng thần kinh nhân tạo không phải dữ liệu tự nhiên, mà là các nhãn chú thích được gắn bởi con người.Việc này làm thay đổi huớng nhân quả: mô hình đang học tác động từ nguyên nhân, vì những nhãn chú thích đó được gây ra bởi các điểm ảnh. Điều này lý giải vì sao dưới góc nhìn của IRM, học có giám sát từ hình ảnh được coi là một vấn đề thuận chiều nhân quả (chứ không phải nghịch chiều nhân quả).
Tuy nhiên, không phải mọi bài toán học có giám sát đều thuận chiều nhân quả. Học có giám sát theo hướng nghịch chiều nhân quả phát sinh khi nhãn không được cung cấp dựa trên các đặc tính, mà dựa trên một số cơ chế khác gây ra các tính năng. Ví dụ, trong hình ảnh y khoa, nhãn có thể được thu thập mà không cần tham chiếu đến chính hình ảnh đó bằng cách quan sát ca bệnh theo thời gian (tuy nhiên đây không phải là cách tiếp cận được khuyến nghị để điều trị).

Học thuận chiều nhân quả giải thích một số thành công của học có giám sát - có khả năng   nó thực sự có thể khôi phục các dạng biểu diễn bất biến mà không cần điều chỉnh. Bất kỳ thuật toán học có giám sát nào cũng học cách kết hợp các đặc tính để dự đoán mục tiêu. Nếu hướng học thuận chiều nhân quả, thì mỗi thuộc tính đầu vào là một nguyên nhân tiềm ẩn của mục tiêu đầu ra và có thể các đặc tính được học là nguyên nhân thực sự. Bên cạnh đó, các điều chỉnh nhằm giảm thiểu rủi ro bất biến đối với quy trình huấn luyện góp phần tăng khả năng khôi phục các dạng biểu diễn bất biến. 









