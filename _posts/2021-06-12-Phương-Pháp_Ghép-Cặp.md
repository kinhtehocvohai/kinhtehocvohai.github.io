---
layout: single
title: Phương Pháp Ghép Cặp
excerpt: "60 GIÂY NHÂN QUẢ - KỲ 2"
toc: false
categories:
  - series 60 giây nhân quả
tags:
  - suy luận nhân quả
permalink: /causalgraph/ac02
sidebar:
    nav: causalgraph
---

**60 GIÂY NHÂN QUẢ - KỲ 2**

*Bài viết này thuộc chuỗi bài viết về “60 Giây Nhân quả”. Hãy cùng đọc thêm các bài viết có cùng chủ đề [tại đây](http://kinhtehocvohai.com/causalgraph/)*

*Để hiểu thêm kiến thức về Suy luận Nhân quả, hãy cùng tìm đọc chuỗi bài viết về “Suy luận Nhân quả với Python” [tại đây](http://kinhtehocvohai.com/pythoncausal/)*


-------

Giả sử có một biến can thiệp chính sách T và chúng ta muốn đánh giá tác động của nó đối với biến kết quả Y. 

Trường hợp lý tưởng, chúng ta chỉ việc nhìn vào mối quan hệ giữa biến Y và can thiệp T và xong việc. 

Nhưng thực tế đâu dễ dàng như vậy? Ví dụ, có những nhóm người dễ hoặc khó nhận can thiệp hơn và những người này thu được kết quả Y cao hơn hoặc thấp hơn bình thường. Giả sử đặc tính X chi phối việc một người có dễ tiếp cận can thiệp T hay không và đồng thời tác động đến biến kết quả Y như đồ thị nhân quả dưới đây:

![image-center](/assets/images/animatedcausality/ac02/output_4_0.svg){: .align-center}

Khi điều này xảy ra, mối quan hệ ta nhìn thấy giữa Can thiệp và kết quả Y từ dữ liệu phản ánh 2 điều: tác động của can thiệp lên Y (cái mà ta quan tâm) và tác động kép của X đối với Can thiệp và Y (cái mà ta không quan tâm). X tạo ra một lối đi cửa sau giữa Can thiệp và kết quả Y. Chúng ta có thể đi từ Can thiệp → Y hoặc Can thiệp ← X → Y.

Ví dụ nếu Can thiệp là việc một thành phố nâng cấp đường giao thông vào 2014 và Y là tăng trưởng GDP của thành phố đó năm 2015. Ta quan sát thấy các thành phố được can thiệp (có nâng cấp đường) tăng trưởng nhanh hơn ở năm tiếp theo so với nhóm đối chứng (các thành phố không nâng cấp đường). Một phần là do việc nâng cấp đường làm tăng GDP nhưng cũng có thể là do các thành phố đang trong đà tăng trưởng nóng có nhiều ngân sách để nâng cấp đường xá hơn. Trong ví dụ này X là tăng trưởng GDP trước 2014.

Một cách để giải quyết vấn đề là đóng lại "cửa sau" bằng cách ghép cặp theo X. Ý tưởng là chúng ta muốn nhìn vào quan hệ giữa Can thiệp và Y giữa các thành phố có giá trị X tương tự nhau. Một cách khác là nhìn vào quan hệ giữa Can thiệp và Y sau khi loại bỏ tác động của X. Bằng cách đo, chúng ta đóng lại con đường Can thiệp ← X → Y, và chỉ giữ lại Can thiệp → Y mà ta quan tâm. Sau khi kiểm soát X, mối quan hệ còn lại giữa Can thiệp và Y là quan hệ nhân quả (giả sử lối đi "cửa sau" duy nhất là qua X).

Làm thế nào để quan sát quan hệ giữa Can thiệp và Y giữa các thành phố có cùng giá trị X. Thao tác ghép cặp giúp so sánh các thành phố được can thiệp với các đối chứng có giá trị gần giống hoặc tương đồng giá trị X

Nếu Can thiệp là một biến nhị phân (chỉ nhận 2 giá trị), việc ghép cặp theo X diễn ra như sau:

![image-center](/assets/images/animatedcausality/ac02/IVweb.gif){: .align-center}

**Lưu ý:** Có nhiều kĩ thuật ghép cặp khác nhau nhưng ý tưởng chủ đạo tương tự phần trình bày trên đây: chúng ta tìm kiếm các đối tượng đối chứng có giá trị tương đồng hoặc gần bằng đối tượng Can thiệp dựa vào các biến quan sát được
{: .notice--warning}

## Ghi chú: 

Trong ví dụ trên, biến Y được tạo lập như sau:

$$Y=3+0.4X+ T + \varepsilon, \varepsilon \sim  N(0,1)$$

Hệ số "thực" của tác động can thiệp T lên Y là +1.

Nếu không ghép cặp:

$$E(Y|T=1)-E(Y|T=0)=1.52$$


## Tạo lập dữ liệu

```python
import warnings
warnings.filterwarnings('ignore')

import pandas as pd
import numpy as np

# Set size
size=200
np.random.seed(0)

# Biến giải thích
X= np.random.uniform(-5,5,size)
Treat=[1]*int(0.1*size)+[0]*int(0.9*size)
Y=3+0.4*X+1*Treat+ np.random.normal(0,1,size)


# Tạo bảng dữ liệu
df=pd.DataFrame({'X':X,'Y':Y,'Treat':Treat})
df1=df[df.Treat==1]
df0=df[df.Treat==0]

```
