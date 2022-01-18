---
layout: single
sidebar:
 nav: aicausal
title: Lời nói dối vĩ đại của học máy
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 9"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac09
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 9**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------

Khi sử dụng học giám sát, chúng ta muốn dự báo điều chưa biết dựa trên thông tin sẵn có. Thông thường, công việc này có thể tóm gọn trong việc kết nối (dữ liệu) đầu vào và đầu ra.

Để làm  điều này, ta cần một tập dữ liệu về các tính năng đầu vào và mục tiêu đầu ra; lượng dữ liệu tỉ lệ với độ phức tạp của vấn đề. Sau đó, ta ước lượng các tham số của thuật toán học máy để tối thiểu hóa hàm mất mát được định sẵn. Ví dụ, khi dự báo một biến liên tục, như nhiệt độ, chúng ta có thể tìm cách giảm thiểu bình phương sai số trung bình  giữa dự báo và các phép thực đo.

Nếu không cẩn thận, các tham số của thuật toán sẽ quá khớp (overfit) với tập dữ liệu. Trong trường hợp này, mô hình quá khớp vì học vẹt các đặc tính cá biệt của tập dữ liệu đó (tương quan giả!). Kết quả là khi mô hình được áp dụng cho bất kỳ tập dữ liệu nào khác (thậm chí với các tập dữ liệu dựa trên cùng một mô hình tạo lập dữ liệu), tính dự báo của mô hình sẽ rất thấp vì những đặc tính quá cá biệt trước đó không còn tồn tại.

Để tránh tình trạng quá khớp, chúng ta sử dụng các thuật toán chính quy hóa (regularition) và điều chỉnh độ phức tạp của mô hình đến một mức thích hợp. Khi ước lượng mô hình, ta cần xáo trộn và chia nhỏ dữ liệu nhằm “học” các thông số từ một phần dữ liệu và xác thực kết quả của mô hình trên phần dữ liệu còn lại. Điều này đảm bảo các tham số tóm gọn thông tin từ toàn bộ dữ liệu mà ta có, chứ không phải chỉ một phần của nó.

Khi sử dụng bất kỳ một quy trình nào (xác thực chéo, chuỗi chuyển tiếp cho dữ liệu chuỗi thời gian hoặc đơn giản hơn là phân chia dữ liệu thành các tệp huấn luyện-thử nghiệm-xác thực), chúng ta đều đang dựa trên một giả định quan trọng. Đó là các điểm dữ liệu độc lập và cùng tuân theo một quy luật phân phối xác suất (i.i.d.). Độc lập thể hiện qua việc mỗi điểm dữ liệu được tạo ra mà không phụ thuộc bất kỳ điểm dữ liệu nào khác. Phân phối giống nhau  nghĩa là phân phối xác suất của mô hình tạo lập dữ liệu giống nhau đối với mọi điểm dữ liệu.

Hãy xem phần thảo luận của Zoubin Ghahramani [tại đây](https://www.youtube.com/watch?v=x1UByHT60mQ&feature=youtu.be&t=37m34s)

Giả định các điểm dữ liệu độc lập và được phân phối giống nhau là lời nói dối vĩ đại của học máy bởi vì dữ liệu hiếm khi có cả hai tính chất trên. Vậy kết cục của học máy là gì khi chúng dựa trên những giả định sai lầm như vậy?

**Sự nguy hiểm của tương quan giả**

Khi huấn luyện một hệ thống học máy với giả định i.i.d., chúng ta đang ngầm giả định một mô hình tạo dữ liệu cơ bản nào đó cho dữ liệu.  Mô hình tạo dữ liệu này thiết lập một môi trường. Các  mô hình tạo dữ liệu khác nhau sẽ tạo ra môi trường khác nhau, với các phân phối xác suất cơ bản khác nhau cho các đặc tính và mục tiêu.

Khi môi trường mà chúng ta dự báo khác với môi trường mà hệ thống học máy được huấn luyện, chúng ta có thể lường trước độ chính xác của mô hình không cao. Mối tương quan giữa các đặc điểm và mục tiêu là khác nhau. Vì vậy, mô hình chúng ta tạo ra để học mối quan hệ giữa các đặc tính và mục tiêu trong một môi trường sẽ đưa ra dự báo không chính xác cho mục tiêu của các đặc tính trong môi trường khác.
Thật không may, ta khó có thể biết liệu mô hình tạo lập dữ liệu cho dữ liệu tại thời điểm dự báo (ví dụ trong hệ thống ML đã triển khai) có giống với trong thời điểm huấn luyện hay không. Ngay cả khi hệ thống đang dự báo rất tốt, nếu chúng ta không hoặc không thể thu thập các nhãn thực để khớp với các đặc điểm đầu vào mà ta dùng để dự báo, chúng ta có thể sẽ không bao giờ kiểm chứng được.

Vấn đề này không phải gì đó quá học thuật. Bài báo “Nhận dạng tại hoang đảo” chỉ ra điều này theo cách hài hước (xem thêm “Cái Nhìn Ngay thẳng vào Tập dữ liệu Thiên lệch”). Cả hai bài báo này đều nhấn mạnh rằng hệ thống thị giác máy tính được đào tạo để nhận dạng trực quan các vật thể, động vật và con người có thể thất bại thê thảm trong việc nhận ra các đối tượng giống nhau trong các bối cảnh khác nhau. Chúng có thể dễ dàng nhận ra một con bò trên cao nguyên, nhưng một con bò trên bãi biển thì hoàn toàn không được chú ý, hoặc được phân loại một cách hời hợt là "động vật có vú".

{% include figure image_path="/assets/images/aicausal/chap3/chap3_recognition.png" caption="*Hình ảnh được trích từ bài báo [Nhận dạng tại hoang đảo](https://arxiv.org/abs/1807.04975), phần chú thích phân tích các đối tượng được cung cấp bởi [ClarifAI](https://user-images.githubusercontent.com/69302326/134803073-a7323b1a-372e-4dee-9628-e6c71e927969.png)
" %}

Những thất bại này không có gì đáng ngạc nhiên! Học máy giám sát được thiết kế để khai thác mối tương quan giữa các đặc điểm nhằm tạo ra năng lực dự đoán, và trong ví dụ này, bò và cao nguyên có mối tương quan cao. Mạng thần kinh là một loại mô hình rất linh hoạt mã hóa các sự bất biến của tập dữ liệu mà dựa vào đó chúng được huấn luyện. Nếu bò xuất hiện chủ yếu trên cỏ, chúng ta kỳ vọng mô hình sẽ học điều này.

**Khi nào thì một mối tương quan là giả?**

Trong học máy giám sát, chúng ta học cách sử dụng các mối tương quan tinh vi, có thể trong không gian đa chiều như hình ảnh tự nhiên, để đưa ra dự báo. Điều gì có thể tách biệt mối tương quan thực sự với mối tương quan giả? Câu trả lời phụ thuộc vào mục đích sử dụng của mô hình kết quả.

Nếu mục đích là để thuật toán chỉ hoạt động trong một môi trường, với các hình ảnh rất giống nhau, thì nên sử dụng tất cả các mối tương quan mà ta có, bao gồm cả những trường hợp rất cá biệt với môi trường của chúng ta. Tuy nhiên, nếu như trong hầu hết mọi trường hợp - chúng ta dự định sử dụng thuật toán trên dữ liệu mới bên ngoài môi trường huấn luyện, chúng ta có thể coi bất kỳ mối tương quan nào chỉ đúng khi ở trong môi trường huấn luyện là tương quan giả. Tương quan giả là một tương quan chỉ đúng do hiệu ứng lựa chọn (chẳng hạn như chọn một tập huấn luyện!).

Trong những phần trước, chúng ta đã thấy rằng mối tương quan có thể phát sinh từ một số cấu trúc nhân quả. Để diễn giải một cách chính xác nhất thì bất kỳ mối tương quan nào không phát sinh từ quan hệ nhân quả trực tiếp đều có thể được coi là giả.

Thật không may, chỉ với một tập dữ liệu huấn luyện hữu hạn, ta thường không thể biết được tương quan nào là giả. Các phương pháp trong phần này nhằm giải quyết xác đáng vấn đề đó.

Khi một thuật toán học máy chủ yếu dựa vào các tương quan giả để dự báo, tính chính xác của nó không cao đối với dữ liệu ngoài tập dữ liệu mà nó được huấn luyện. Tuy nhiên, đó không phải là vấn đề duy nhất với tương quan giả.

Ngày càng có nhiều sự quan tâm về khả năng diễn giải học máy. Một hệ thống học máy không chỉ nên đưa ra dự báo mà còn nên cung cấp phương tiện để đánh giá xem những dự báo đó đã được thực hiện như thế nào. Nếu một mô hình đang dựa trên các tương quan giả, thì tính quan trọng của các đặc điểm (chẳng hạn như các giá trị được tính toán bởi LIME hoặc SHAP) cũng sẽ là giả mà thôi. Chính vì vậy không nên đưa ra quyết định nào dựa trên những lời giải thích giả!



