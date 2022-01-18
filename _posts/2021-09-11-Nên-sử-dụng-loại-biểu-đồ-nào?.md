---
layout: single
sidebar:
 nav: aicausal
title: Nên sử dụng loại biểu đồ nào?
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 8"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac08
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 8**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Nhận biết cấu trúc nhân quả thực của vấn đề nghiên cứu rất quan trọng. Ở những kỳ trước chúng ta đã tìm hiểu ba cấu trúc chính của biểu đồ nhân quả bao gồm: cấu trúc trực tiếp, hình dĩa (hay gốc chung) và đỉnh va chạm (hay đích chung). Tuy nhiên trong thực tế, biểu đồ có thể bao gồm các cấu trúc trung gian phức tạp khác.

Cấu trúc biểu đồ cho phép ta suy luận một cách định tính về các mối phụ thuộc thống kê trong dữ liệu. Trong trường hợp không có thử nghiệm ngẫu nhiên đối chứng hoặc các thử nghiệm khác, ta sẽ cần tới tư duy định tính để suy luận nhân quả. Chúng ta cần sử dụng kiến thức nghiệp vụ của mình để xây dựng một biểu đồ hợp lý, sau đó kiểm thử nó trên dữ liệu sẵn có. Một biểu đồ có thể bị bác bỏ bằng cách xem xét các mối quan hệ độc lập về mặt thống kê mà nó biểu hiện, và so sánh chúng với những mối quan hệ được kỳ vọng từ cấu trúc nhân quả. Ví dụ, nếu hai biến kết nối với nhau   qua một tác nhân chung không bị kiểm soát, ta có thể kỳ vọng vào sự phụ thuộc về mặt thống kê giữa chúng. 

**Khám phá nhân quả**

Các mối quan hệ độc lập trong một biểu đồ có thể được sử dụng để khám phá quan hệ nhân quả. Đó là quá trình nỗ lực khôi phục biểu đồ nhân quả từ dữ liệu quan sát. Có nhiều cách tiếp cận phù hợp với các giả định khác nhau về biểu đồ. Tuy nhiên, vì các biểu đồ nhân quả khác nhau có thể cùng biểu thị một phân phối xác suất đồng thời, nên điều tốt nhất ta có thể kỳ vọng từ quá trình khám phá nhân quả là một tập hợp các biều đồ hợp lý, và nếu may mắn, biểu đồ thực  nằm trong số đó. Thực tế, không phải lúc nào cũng có thể suy ra hướng của quan hệ nhân quả chỉ từ dữ liệu ngay cả trong một hệ thống chỉ gồm hai biến.

Nhìn chung, không thể chứng minh tính đúng đắn của một biểu đồ nhân quả cụ thể, vì các biểu đồ khác nhau vẫn có thể dẫn đến cùng một phân phối quan sát thậm chí là phân phối can thiệp. Chính vì việc xác định quan hệ nhân quả là không dễ dàng nên chúng ta cần thận trọng khi đưa ra các kết luận về quan hệ nhân quả. Có lẽ cách tốt nhất để nhìn nhận mô hình nhân quả là đưa ra các kết quả có điều kiện dựa trên một tập hợp các giả định nhân quả. Hai nút không kết nối trực tiếp trong biểu đồ nhân quả được giả định là độc lập trong quá trình tạo lập dữ liệu, ngoại trừ các quan hệ nhân quả được mô tả ở phía trên (về phía gốc), hoặc sự kết hợp của chúng tạo ra sự phụ thuộc về mặt thống kê. 

Tính đúng đắn của kết quả phụ thuộc vào tính đúng đắn của các giả định. Tất nhiên, chúng ta phải đối mặt với mctình huống chung trong các bài toán học máy, và có thể kỳ vọng rằng các khẳng định nhân quả mạnh hơn đòi hỏi các giả định mạnh hơn  các khẳng định quan sát đơn thuần.


{% include figure image_path="/assets/images/aicausal/chap2/whichgraph.png"%}

Đôi khi khó có thể thiết lập hướng nhân quả ngay cả trong các biểu đồ rất đơn giản.

Một trường hợp mà chúng ta có thể xác định biểu đồ nhân quả thực là khi chúng ta tự tạo ra hệ thống. Ví dụ,  với một dây chuyền sản xuất có một quy trình xác định đầy đủ, ta có thể phác thảo một sơ đồ mã hoá hướng dây chuyền giữa các máy móc. Sơ đồ đó là tiền đề rất tốt cho việc thiết lập biểu đồ nhân quả. Nếu chúng ta lập mô hình sản xuất có các bộ phận bị lỗi, biểu đồ đó sẽ là cơ sở tốt cho biểu đồ nhân quả. Vì một thiết bị chưa xử lý sản phẩm lỗi sẽ không chịu trách nhiệm cho lỗi đó, và đồ thị nhân quả mã hoá chính xác mối quan hệ độc lập này.

**Ý tưởng chính**

Mô hình biểu đồ nhân quả trình bày một phương pháp lý luận trực quan và hữu ích cho hệ thống cũng như cách thế giới vận hành. Trong trường hợp một bài toán dự báo thuần tuý, cách lý luận này có thể không cần thiết, và chúng ta có thể áp dụng phương pháp học có giám sát để khai thác các quan hệ tương quan tiềm ẩn giữa các biến và đối tượng cần dự báo. Tuy nhiên, khi dự báo được dùng để đưa ra quyết định làm thay đổi hệ thống, hoặc dự báo cho hệ thống đang bị can thiệp, chúng ta phải sử dụng suy luận nhân quả để tránh việc đưa ra những kết luận không chính xác. Đằng sau mỗi kết luận nhân quả luôn có một giả định nhân quả không thể kiểm chứng hoặc xác minh bằng quan sát đơn thuần.

Ngay cả khi chưa có kiến thức bài bản về suy luận nhân quả, suy luận định tính dựa trên mô hình biểu đồ nhân quả vẫn có tác dụng nhất định. Việc cố gắng xây dựng một biểu đồ nhân quả buộc chúng ta phải tư duy về cách mô hình hệ thống, và góp phần làm rõ các lỗi thống kê và diễn giải tiềm ẩn. Hơn nữa, nó mã hoá chính xác các giả định độc lập mà chúng ta đưa ra. Tuy nhiên, các biểu đồ này có thể phức tạp và nhiều chiều, đồng thời đòi hỏi sự hợp tác chặt chẽ giữa người nghiên cứu nhân quả và các chuyên gia có nghiệp vụ và  kiến thức chuyên sâu về hệ thống.

Trong nhiều lĩnh vực, các vấn đề như quá nhiều biến dự báo, kích thước mẫu nhỏ, khả năng xuất hiện của những nguyên nhân không đo lường được là những rào cản lớn trong việc áp dụng suy luận nhân quả trong thực tế. Trong những trường hợp này, một lượng giới hạn kiến thức nền tảng cũng có thể giúp giảm bớt số lượng các giả thuyết nhân quả. Ngay cả việc  tiến hành can thiệp thử nghiệm là có thể thì việc tiến hành hàng nghìn thử nghiệm để khám phá mối quan hệ nhân quả giữa hàng nghìn hoặc hàng chục nghìn biến dự báo lại không khả thi. 

Trước những thách thức này, làm thế nào chúng ta có thể kết hợp suy luận nhân quả và học máy? Nhiều phương pháp tiếp cận “vùng giao” giữa học máy và suy luận nhân quả được thúc đẩy bởi khả năng áp dụng các kỹ thuật suy luận nhân quả cho dữ liệu nhiều chiều, và trong các lĩnh vực khó xác định quan hệ nhân quả. Trong những kỳ tới, chúng ta sẽ cùng tìm hiểu cách thu hẹp khoảng cách này giữa các mô hình nhân quả cấu trúc và học máy có giám sát. 



