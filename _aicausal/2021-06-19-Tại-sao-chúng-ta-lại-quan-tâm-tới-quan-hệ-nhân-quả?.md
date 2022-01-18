---
layout: single
sidebar:
 nav: aicausal
title: Tại sao chúng ta lại quan tâm tới quan hệ nhân quả?
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 2"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac02
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 2**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Hãy xem xét trường hợp một ngân hàng muốn giảm số lượng các khoản vay bị vỡ nợ. Dữ liệu lịch sử và các mô hình học máy giám sát tinh vi có thể xác định chính xác khoản vay nào có khả năng vỡ nợ, và các kỹ thuật diễn giải có thể cho ta biết một số đặc điểm liên quan đến (hoặc tiên lượng) khả năng vỡ nợ. Tuy nhiên, để giảm tỷ lệ vỡ nợ chúng ta phải biết những thay đổi cần làm, điều này không chỉ đòi hỏi việc nhận diện các khoản vay vỡ nợ, mà cả lý do tại sao khoản vay đó vỡ nợ.

Chúng ta có thể quan sát thấy các khoản vay nhỏ có khả năng vỡ nợ cao hơn các khoản vay lớn. Một suy luận non nớt có thể đề xuất ngân hàng ngừng cho vay các khoản nhỏ. Tuy nhiên, thực tế có thể là do các doanh nghiệp nhỏ dễ phá sản hơn các doanh nghiệp lớn, và đồng thời học thường vay các khoản nhỏ hơn. Trong trường hợp này, mối quan hệ nhân quả thực sự là mối quan hệ giữa quy mô khách hàng doanh nghiệp và khả năng vỡ nợ, chứ không phải giữa quy mô khoản vay và khả năng vỡ nợ. Khi đó các quyết định về chính sách của ngân hàng nên nhắm tới quy mô doanh nghiệp thay vì quy mô khoản vay. 

Thật không may, mô hình học máy giám sát không cho ta biết mối quan hệ nhân quả thật sự. Nếu đưa vào mô hình cả quy mô khoản vay và quy mô doanh nghiệp như những thuộc tính, chúng ta sẽ chỉ nhận thấy cả hai phần nào đều liên quan đến khả năng vỡ nợ. Mặc dù quan sát này đúng (vì cả hai đều có tương quan thống kê tới khả năng vỡ nợ), câu hỏi mà chúng ta quan tâm về nguyên nhân gây ra vỡ nợ vẫn chưa có câu trả lời. 

Quan hệ nhân quả cung cấp cho chúng ta khung lý luận để giải quyết những câu hỏi như vậy. Những nghiên cứu gần đây về sự giao thoa giữa quan hệ nhân quả và học máy giúp cho việc khám phá các mối quan hệ nhân quả trở nên dễ dàng hơn.

**Những điểm yếu của mô hình học máy giám sát**

Không thể phủ nhận sự thành công của mô hình học máy giám sát trong rất nhiều  tác vụ, đặc biệt khi xử lý các bài toán yêu cầu đầu vào dữ liệu nhiều chiều, chẳng hạn như thị giác máy tính và xử lý ngôn ngữ tự nhiên. Đã có nhiều tiến bộ đáng chú ý trong hai thập kỷ qua và cần lưu ý việc nhận diện các thiếu sót của mô hình học máy giám sát không có ý  xem nhẹ những tiến bộ đó theo bất kỳ hình thức nào.

Sự thành công của mô hình học giám sát đã làm tăng sự kỳ vọng vào các hệ thống tự động có khả năng đưa ra những quyết định độc lập và thậm chí sở hữu trí tuệ như con người. Các phương pháp tiếp cận học máy hiện tại chưa thể đáp ứng những kỳ vọng đó do còn tồn tại những hạn chế cơ bản của việc nhận dạng mẫu (pattern recognition).

Đầu tiên đó là tính khái quát hoá (hay còn gọi là  độ mạnh hay khả năng thích ứng), là khả năng áp dụng một mô hình trong bối cảnh hay môi trường mới. Nhiều phương pháp học máy hiện đại giả định sẽ áp dụng mô hình được huấn luyện cho dữ liệu giống với dữ liệu trong tập huấn luyện. Các mô hình này được huấn luyện cho các tác vụ cụ thể, như phân biệt hình ảnh chó hoặc mèo, hay phát hiện gian lận trong giao dịch ngân hàng. Tuy nhiên, thực tế dữ liệu mà chúng ta sử dụng cho dự đoán thường khác với dữ liệu trong tập huấn luyện. Ví dụ, dữ liệu huấn luyện thường chịu ảnh hưởng của thiên lệch chọn và việc thu thập thêm dữ liệu cũng không làm giảm thiên lệch.

{% include figure image_path="/assets/images/aicausal/chap2/ac02.png" %}

Một hạn chế khác là khả năng giải thích hay tính tường minh của mô hình. Các mô hình học máy chủ yếu vẫn là các “hộp đen” (black box), có nghĩa là chúng không có khả năng giải thích lý do đưa ra dự báo hay đề xuất của mình. Điều này làm dấy lên câu hỏi làm thế nào người dùng có thể tin tưởng mô hình học máy và gây ra khó khăn cho việc áp dụng trong thực tế. Ví dụ, một mô hình học sâu có thể được huấn luyện để phát hiện ung thư dựa vào các hình ảnh y khoa với độ chính xác cao, miễn là mô hình được cung cấp hình ảnh với số lượng lớn và có đủ năng lực tính toán. Tuy nhiên mô hình không thể thay thế một bác sĩ thực sự vì nó không thể giải thích tại sao hay bằng cách nào mà một hình ảnh cụ thể chỉ báo nguy cơ gây bệnh. Một số phương pháp để giải thích các dự báo của mô hình học máy đã được phát triển. Tuy sự ra đời của những phương pháp này là cần thiết và đáng được hoan nghênh, việc hiểu cách diễn giải mô hình và các hạn chế của chúng cũng là một lĩnh vực kho học [khó nhằn]. Mặc dù các phương pháp như LIME (Phép diễn giải cục bộ cho mô hình bất khả tri) hay SHAP (Lý giải tăng tiến Shapley) rất hữu ích, nhưng chúng chỉ diễn giải chi tiết về cách mô hình hoạt động chứ không phải cách mà thế giới vận hành. 

Và cuối cùng, sự hiểu biết về các mối quan hệ nhân quả, yếu tố thiết yếu của trí thông minh con người, lại thiếu vắng trong các hệ thống nhận dạng mẫu. Con người có khả năng trả lời các loại câu hỏi như “điều gì sẽ xảy ra nếu”. Điều gì sẽ xảy ra nếu tôi thay đổi một điều gì đó? Điều gì sẽ xảy ra nếu tôi hành động khác đi? Những câu hỏi mang tính can thiệp, phản thực, và hồi tưởng như vậy là thế mạnh của trí thông minh con người. Trong khi xây dựng mô hình học máy với loại trí thông minh này vẫn còn là điều xa vời, các nhà nghiên cứu ngày càng nhận ra tầm quan trọng của những câu hỏi nhân quả như vậy và sử dụng chúng với mục đích cung cấp thông tin cho  quá trình nghiên cứu.

Nhìn chung hệ thống học máy giám sát phải được áp dụng một cách thận trọng trong những tình huống nhất định. Nếu chúng ta muốn giảm thiểu những hạn chế trong việc áp dụng học máy, thì chìa khoá chính là quan hệ nhân quả. 


