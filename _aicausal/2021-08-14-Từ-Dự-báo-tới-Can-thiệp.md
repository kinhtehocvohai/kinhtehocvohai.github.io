---
layout: single
sidebar:
 nav: aicausal
title: Từ Dự báo tới Can thiệp
excerpt: "SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 6"
toc: false
categories:
  - series suy luận nhân quả với học máy
tags:
  - suy luận nhân quả
  - học máy
  - khoa học dữ liệu
permalink: /aicausal/ac06
---

**SUY LUẬN NHÂN QUẢ CHO HỌC MÁY - KỲ 6**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả cho Học máy”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/aicausal/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/) và "60 Giây Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/causalgraph/)*


-------


Ở những kỳ trước, chúng ta đã phần nào hiểu được mô hình nhân quả là gì. Trong chương này, chúng ta có thể đi vào phần cốt lõi của nhân quả: sự khác biệt giữa quan sát và can thiệp.

Khái niệm sự can thiệp, một hành động làm thay đổi hệ thống, đã được đề cập trong kỳ trước khi giới thiệu về bậc thang nhân quả. Đây là một hành động cơ bản, nhưng điều quan trọng là ta phải nắm được sự khác biệt giữa can thiệp và quan sát. Sự can thiệp có tính chủ quan hay không? Ai có thể định nghĩa can thiệp là gì?

Hiểu một cách đơn giản, sự can thiệp là một tác động làm thay đổi quá trình tạo lập dữ liệu. Chúng ta có thể thu được mẫu từ phân phối đồng thời của các biến trong biểu đồ đơn giản bằng cách “di chuyển về phía trước theo biểu đồ”. Đối với mỗi nguyên nhân, chúng ta lấy mẫu từ phân phối nhiễu của nó và thay giá trị đó vào Mô hình Nhân quả cấu trúc (SCM) để tính toán kết quả tác động. Để tính toán phân phối can thiệp, chúng ta gán giá trị cụ thể cho các nguyên nhân đang được can thiệp và đưa các giá trị đó vào các phương trình của SCM. Quá trình này dẫn tới sự xuất hiện của một phân phối khác với phân phối quan sát mà chúng ta thường gặp.

Đôi khi có sự nhầm lẫn giữa phân phối can thiệp và phân phối có điều kiện. Phân phối có điều kiện được tạo bằng cách đặt điều kiện lên phân phối quan sát để đáp ứng một số tiêu chí. Ví dụ, chúng ta có thể muốn biết tỷ lệ vỡ nợ của các doanh nghiệp với một mức lãi suất cụ thể. Bản thân lãi suất này có thể đã được xác định bởi một mô hình nào đó, trong trường hợp này, các doanh nghiệp với cùng mức lãi suất đó nhiều khả năng có những điểm tương đồng về mặt thống kê. 

Phân phối can thiệp (ví dụ khi chúng ta can thiệp vào lãi suất) về cơ bản có sự khác biệt. Đó là phân phối của các khoản vay vỡ nợ  khi chúng ta cố định lãi suất ở một giá trị cụ thể ngay cả khi các đặc tính khác của doanh nghiệp có thể đóng góp vào một mức lãi suất khác. Điều này tương ứng với việc loại bỏ tất cả các mũi tên đến lãi suất trong biểu đồ nhân quả, chúng ta đang gán các giá trị sao cho nó không còn phụ thuộc vào các nút “cha mẹ” có quan hệ nhân quả trực tiếp với nó nữa.

Rõ ràng, không phải tất cả các biện pháp can thiệp đều có thể thực hiện được. Mặc dù chúng ta có thể can thiệp để thiết lập mức lãi suất định sẵn, nhưng chúng ta không thể hô biến mọi doanh nghiệp thành doanh nghiệp có quy mô lớn.

### Can thiệp với Python code

Chúng ta có thể  dễ dàng tìm hiểu kĩ hơn về can thiệp với Python. Quay trở lại ví dụ về nút giao, để tính toán phân phối can thiệp, ta có thể xác định một hàm tạo mẫu mới. Điều này có nghĩa là thay vì lấy tất cả các biến một cách ngẫu nhiên, ta có thể can thiêp để gán một giá trị cụ thể cho $$x$$. Bởi vì đây là can thiệp, không chỉ đơn giản là đặt điều kiện như trước đó, chúng ta phải thực hiện thay đổi, sau đó chạy lại quá trình tạo lập dữ liệu.

Thực hiện can thiệp này tạo ra phân phối mới cho $$z$$, khác với phân phối mà chúng ta quan sát được trươc đó. Hơn nữa, mối quan hệ giữa $$x$$ và $$y$$ đã thay đổi. Phân phối đồng thời bây giờ chỉ đơn giản là phân phối biên của $$y$$ vì $$x$$ cố định. Mối quan hệ này hoàn toàn khác so với khi chúng ta đơn giản chỉ đặt điều kiện lên phân phối quan sát.


```python
from numpy.random import randn

def y():
  return 5 + randn()

def z(x, y):
  return x + y + randn()

def sample_intervened():
  x_ = -3
  y_ = y()
  z_ = z(x_, y_)
  return x_, y_, z_
```


```python
import random
random.seed(10)
x_sample, y_sample, z_sample = [], [], []
for i in range(20000):
    data = sample_intervened()
    x_0, y_0, z_0 = data[0], data[1], data[2]
    x_sample.append(x_0)
    y_sample.append(y_0)
    z_sample.append(z_0)
    
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('seaborn-white')

fig, ((ax1, ax2)) = plt.subplots(1, 2, figsize=(9,5))

kwargs = dict(histtype='stepfilled', alpha=0.3, bins=30)

ax1.hist(x_sample, **kwargs, label = 'x', edgecolor='steelblue', linewidth=2)
ax1.hist(y_sample, **kwargs, label = 'y')
ax1.hist(z_sample, **kwargs, label = 'z')
ax1.set_xlim([-10, 10])
ax1.set_ylim([0, 2500])
ax1.set_xlabel('giá trị', fontsize=12)
ax1.set_ylabel('số lượng mẫu', fontsize=12)
ax1.legend(loc='upper right')

ax2.scatter(x_sample, y_sample, alpha=0.3)
ax2.set_xlim([-10, 0])
ax2.set_ylim([0, 10])
ax2.set_xlabel('x', fontsize=12)
ax2.set_ylabel('y', fontsize=12)
plt.savefig('chap2_intervention.png')
plt.show()

```


{% include figure image_path="/assets/images/aicausal/chap3/ac06.png"%}

Bên trái: Chúng ta can thiệp để cố định $$x$$ trong quá trình tạo lập dữ liệu. Điều này dẫn tới $$z$$ thay đổi, nhưng $$y$$ không đổi.
Bên phải: Khi chúng ta can thiệp vào $$x$$, phân phối đồng thời của $$x$$ và $$y$$ trở thành phân phối biên của $$y$$. 

### Ý tưởng chính

Cuối cùng chúng ta thể tóm tắt lại ý tưởng chính của bài viết này với biểu đồ sau:

{% include figure image_path="/assets/images/aicausal/chap3/ac06_1.png"%}

Trước hết hãy xem xét tất cả các câu hỏi bạn muốn giải đáp dựa trên một bộ dữ liệu cụ thể (các mẫu thu được từ một phân phối đồng thời). Việc lấy mẫu từ phân phối đồng thời cho phép ta giải đáp được nhiều câu hỏi và tác vụ. Ví dụ ta có thể thực hiện mô hình học máy có giám sát bằng cách ước lượng phân phối có điều kiện của một biến $$y$$ trên biến $$x$$, và sử dụng kết quả này trong rất nhiều lĩnh vực ứng dụng, ví dụ gắn nhãn hình ảnh. Những câu hỏi dạng này nằm trong phần hình tròn màu xanh. 

Tuy nhiên, chúng ta có thể bắt gặp nhiều câu hỏi không thể trả lời được nếu chỉ dùng dữ liệu/ phân phối đồng thời. Cụ thể, nếu ta muốn đưa ra dự đoán về cách hoạt động của hệ thống chúng ta đang nghiên cứu dưới một số can thiệp nhất định, ta sẽ không thể hoàn toàn suy đoán dựa vào dữ liệu sẵn có. Những câu hỏi như này nằm ngoài hình tròn màu xanh. Để giải quyết các câu hỏi này, bạn có thể cần bổ sung dữ liệu của mình bằng các giả định nhân quả được mã hoá trong biểu đồ nhân quả. Các câu hỏi được trả lời bằng việc khai thác các giả định bổ sung được hiện thị bằng màu vàng. 

Trong phần tiếp theo, chúng ta sẽ tiếp tục tìm hiểu một ví dụ cụ thể về can thiệp trong trường hợp ta cần phải thiết lập mô hình tỷ lệ khách hàng rời đi. Sau đó, chúng ta sẽ cùng hướng tới việc trả lời cho một câu hỏi  vô cùng quan trọng: Khi nào ta cần tới can thiệp và nhân quả? 

*Bài viết có tham khảo thêm từ [inference](https://www.inference.vc/causal-inference-2-illustrating-interventions-in-a-toy-example/)*