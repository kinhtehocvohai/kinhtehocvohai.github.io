---
layout: single
title: Phép thử Ngẫu nhiên
excerpt: "SUY LUẬN NHÂN QUẢ VỚI PYTHON - KỲ 2"
permalink: /pythoncausal/pc02
categories:
  - series suy luận nhân quả với python
tags:
  - suy luận nhân quả
  - python
sidebar:
    nav: pythoncausal
author_profile: true
---

**SUY LUẬN NHÂN QUẢ VỚI PYTHON - KỲ 2**

*Bài viết này thuộc chuỗi bài viết về “Suy luận Nhân quả với Python”. Hãy cùng đọc thêm các bài viết có cùng chủ đề tại [đây](http://kinhtehocvohai.com/pythoncausal/)*

[Nguyên tác: Matheus Facure, chuyển ngữ: Nhóm Kinh tế học Vô hại, dữ liệu và Jupyter Notebook lưu trữ tại [GitHub](https://github.com/vietecon/NhanQuaPython/tree/main/ipynb).]


## Tiêu chuẩn Vàng

Trong phần trước, chúng ta đã thấy lý do tại sao quan hệ tương quan khác với quan hệ nhân quả. Bên cạnh đó, chúng ta cũng đã biết điều kiện cần để biến quan hệ tương quan thành quan hệ nhân quả.

$$E[Y|T=1] - E[Y|T=0] = \underbrace{E[Y_1 - Y_0|T=1]}_{ATET}$$ 

$$+ \underbrace{\{ E[Y_0|T=1] - E[Y_0|T=0] \}}_{THIÊN LỆCH}$$

Tóm lại, quan hệ tương quan sẽ trở thành quan hệ nhân quả nếu không có thiên lệch. Thiên lệch sẽ không tồn tại nếu \\(E[Y_0\|T=0]=E[Y_0\|T=1]\\). Nói cách khác, quan hệ tương quan sẽ là quan hệ nhân quả nếu các nhóm được can thiệp và nhóm đối chứng là như nhau, hoặc tương đồng, ngoại trừ việc chúng có được nhận can thiệp hay không. Về mặt kỹ thuật, kết quả của nhóm đối chứng bằng với kết quả giả tưởng của nhóm được can thiệp. Trong đó, kết quả giả tưởng là kết quả của nhóm can thiệp trong trường hợp không có sự can thiệp.

Chúng ta đã giải thích ổn thoả về việc làm thế nào để quan hệ tương quan trở thành quan hệ nhân quả bằng các công thức toán học. Nhưng tất cả cũng mới là trên lý thuyết. Ngay bây giờ, chúng ta sẽ tìm hiểu công cụ đầu tiên mà chúng ta có nhằm xoá bỏ thiên lệch: **Thử Nghiệm Đối Chứng Ngẫu Nhiên**. Các thử nghiệm đối chứng ngẫu nhiên bao gồm việc chỉ định một cách ngẫu nhiên các cá thể trong một tổng thể vào nhóm can thiệp hoặc nhóm đối chứng. Tỉ lệ nhận sự can thiệp không nhất thiết phải là 50%. Các bạn có thể có một thử nghiệm khi mà chỉ có 10% mẫu được nhận sự can thiệp.


Thử nghiệm ngẫu nhiên loại bỏ thiên lệch bằng cách làm cho các kết quả tiềm năng độc lập với sự can thiệp.

$$
(Y_0, Y_1) \perp\!\!\!\perp T
$$

Nhìn qua thì công thức này có thể rắc rối (kể cả với chúng tôi). Nhưng hãy yên tâm vì chúng tôi sẽ đi sâu vào việc giải thích công thức này ngây bây giờ. Nếu kết quả độc lập với sự can thiệp, không phải điều này đang ám chỉ rằng sự can thiệp đó không có tác dụng gì cả hay sao? Vâng, đúng vậy đấy! nhưng hãy chú ý rằng chúng tôi không nói về các kết quả thực sự xảy ra. Thay vào đó, chúng tôi đang bàn về các **kết quả tiềm năng**. Kết quả tiềm năng chính là kết quả có thể sẽ xảy ra trong trường hợp có sự can thiệp (\\(Y_1\\)) hoặc kiểm soát (\\(Y_0\\)). Đối với các thử nghiệm ngẫu nhiên, chúng ta **không** muốn kết quả độc lập với sự can thiệp, bởi vì chúng ta cho rằng sự can thiệp chi phối kết quả. Nhưng chúng ta lại muốn các **kết quả tiềm năng** độc lập với sự can thiệp.

![image-center](/assets/images/pythoncausal/rct/indep.png){: .align-center}

Nói rằng các kết quả tiềm năng độc lập với sự can thiệp cũng có nghĩa là chúng ta kỳ vọng chúng giống nhau dù trong nhóm can thiệp hay nhóm đối chứng. Hiểu một cách đơn giản thì các nhóm can thiệp và nhóm đối chứng là tương tự. Hoặc việc chỉ định sự can thiệp không cung cấp cho chúng ta bất cứ thông tin nào về kết quả trước khi có sự can thiệp. Vậy nên, \\((Y_0, Y_1)\perp T\\) có nghĩa sự can thiệp này là thứ duy nhất tạo ra sự khác biệt giữa kết quả trong nhóm được can thiệp và nhóm đối chứng. Để thấy được điều này, cần chú ý rằng tính độc lập ngụ ý một cách chính xác rằng 

$$
E[Y_0|T=0]=E[Y_0|T=1]=E[Y_0]
$$

Như chúng ta đã thấy, điều này có thể được biểu diễn thành

$$
E[Y|T=1] - E[Y|T=0] = E[Y_1 - Y_0]=ATE
$$

Như vậy, thử nghiệm ngẫu nhiên đưa ra cách sử dụng sự khác biệt giản đơn giữa các giá trị bình quân của nhóm can thiệp và nhóm đối chứng, hay còn được gọi là hiệu ứng can thiệp.


## Tại một ngôi trường xa thật xa

Trong năm 2020, đại dịch vi-rút Corona đã buộc các doanh nghiệp phải thích nghi với giãn cách xã hội. Các dịch vụ giao hàng đã trở nên phổ biến, những doanh nghiệp lớn đã chuyển sang chiến lược làm việc từ xa. Các trường học không nằm ngoài xu hướng đó. Rất nhiều trường đã bắt đầu tổ chức các lớp học trực tuyến.

Bốn tháng kể từ bắt đầu khủng hoảng, nhiều người đang thắc mắc rằng liệu những thay đổi trên có thể được duy trì hay không. Những lợi ích của giáo dục trực tuyến là không thể bàn cãi. Cụ thể là chi phí thấp hơn, có thể tiết kiệm được chi phí mặt bằng và đi lại. Giáo dục trực tuyến mang tính số hoá, tận dụng tối đa được các bài giảng có chất lượng tốt nhất trên toàn cầu, không còn chỉ gói gọn trong một nhóm giáo viên cố định. Tuy nhiên, chúng ta vẫn cần câu trả lời cho việc liệu học trực tuyến có ảnh hưởng tiêu cực hoặc tích cực đến thành tích học tập của học sinh hay không.

Một cách để trả lời vấn đề này là lấy những học sinh từ các trường chủ yếu dạy trực tuyến và so sánh với những học sinh từ các trường dạy theo phương pháp truyền thống. Như chúng ta đã biết cho đến hiện tại đây không phải là cách tiếp cận tốt nhất. Có thể do các trường trực tuyến chỉ thu hút những học sinh tự giác, do vậy kết quả học tập của nhóm học sinh này cao hơn mức trung bình ngay cả khi chúng tham gia lớp học truyền thống. Trong trường hợp này, chúng ta có thể đã mắc phải một thiên lệch dương, khi mà nhóm được can thiệp có năng lực học vấn tốt hơn nhóm đối chứng: \\(E[Y_0\|T=1] > E[Y_0\|T=0]\\). 

Mặt khác, cũng có thể do các lớp học trực tuyến rẻ hơn và tập trung hầu hết các học sinh không có điều kiện và có thể phải vừa học vừa làm. Trong trường hợp trên, những học sinh này sẽ học kém hơn các bạn kể cả khi chúng theo học các lớp học truyền thống. Nếu điều này xảy ra, chúng ta đã bị thiên lệch theo hướng ngược lại, khi mà nhóm được can thiệp có năng lực học vấn kém hơn nhóm đối chứng: \\(E[Y_0\|T=1] < E[Y_0\|T=0]\\).

Vì vậy, mặc dù chúng ta có thể làm các phép so sánh đơn giản, chúng sẽ không đủ sức thuyết phục. Bằng cách này hay cách khác, chúng ta không bao giờ có thể chắc chắn được liệu rằng có bất kỳ sự thiên lệch nào đang ẩn nấp quanh đây và che đậy tác động nhân quả hay không.

![image-center](/assets/images/pythoncausal/rct/lurking_bias.png){: .align-center}

Để giải quyết, chúng ta cần phải làm cho nhóm được can thiệp và nhóm đối chứng trở nên tương đồng \\(E[Y_0\|T=1] = E[Y_0\|T=0]\\). Một biện pháp nhằm đạt được điều kiện trên là chỉ định một cách ngẫu nhiên các lớp học trực tuyến và truyền thống cho học sinh. Nếu chúng ta làm được điều đó, thì bình quân các nhóm can thiệp và đối chứng sẽ trở nên tương tự, ngoại trừ việc trẻ có được nhận can thiệp hay không.

May mắn thay, một số nhà kinh tế học đã làm điều đó cho chúng ta. Họ đã chọn ngẫu nhiên các lớp học, chứ không phải học sinh. Một số học sinh được chỉ định ngẫu nhiên vào các bài giảng theo hình thức truyền thống, một số học sinh khác chỉ tham gia các bài giảng trực tuyến, và nhóm học sinh thứ ba tham gia loại hình giảng dạy được kết hợp bởi cả các bài giảng trực tuyến và truyền thống. Vào cuối học kỳ, họ đã thu thập dữ liệu về một kỳ thi chuẩn hoá.

Và đây chính là dữ liệu thu thập được:



```python
import pandas as pd
import numpy as np

data = pd.read_csv("./data/online_classroom.csv")
print(data.shape)
data.head()
```

    (323, 10)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender</th>
      <th>asian</th>
      <th>black</th>
      <th>hawaiian</th>
      <th>hispanic</th>
      <th>unknown</th>
      <th>white</th>
      <th>format_ol</th>
      <th>format_blended</th>
      <th>falsexam</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>63.29997</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>79.96000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>83.37000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>90.01994</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>83.30000</td>
    </tr>
  </tbody>
</table>
</div>



Chúng ta có thể thấy có tất cả 323 quan sát. Đây không hẳn là một bộ dữ liệu lớn, nhưng vẫn đủ để chúng ta có thể sử dụng. Để ước lượng tác động nhân quả, chúng ta chỉ cần tính điểm số trung bình cho mỗi nhóm can thiệp. 


```python
(data
 .assign(class_format = np.select(
     [data["format_ol"].astype(bool), data["format_blended"].astype(bool)],
     ["online", "blended"],
     default="face_to_face"
 ))
 .groupby(["class_format"])
 .mean())
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender</th>
      <th>asian</th>
      <th>black</th>
      <th>hawaiian</th>
      <th>hispanic</th>
      <th>unknown</th>
      <th>white</th>
      <th>format_ol</th>
      <th>format_blended</th>
      <th>falsexam</th>
    </tr>
    <tr>
      <th>class_format</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>blended</th>
      <td>0.550459</td>
      <td>0.217949</td>
      <td>0.102564</td>
      <td>0.025641</td>
      <td>0.012821</td>
      <td>0.012821</td>
      <td>0.628205</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>77.093731</td>
    </tr>
    <tr>
      <th>face_to_face</th>
      <td>0.633333</td>
      <td>0.202020</td>
      <td>0.070707</td>
      <td>0.000000</td>
      <td>0.010101</td>
      <td>0.000000</td>
      <td>0.717172</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>78.547485</td>
    </tr>
    <tr>
      <th>online</th>
      <td>0.542553</td>
      <td>0.228571</td>
      <td>0.028571</td>
      <td>0.014286</td>
      <td>0.028571</td>
      <td>0.000000</td>
      <td>0.700000</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>73.635263</td>
    </tr>
  </tbody>
</table>
</div>



Vâng. Chỉ đơn giản vậy thôi. Chúng ta có thể thấy các lớp học truyền thống có số điểm trung bình là 78.54, trong khi các lớp học trực tuyến cho số điểm trung bình là 73.63. Đây quả thật không phải là một tin tốt lành cho những tín đồ của việc học trực tuyến. Vì vậy \\(ATE\\) cho lớp học trực tuyến là -4.91. Điều này có nghĩa là bình quân **các lớp học trực tuyến làm cho học sinh thể hiện kém hơn khoảng 5 điểm**. Như vậy, bằng cách này các bạn không cần phải băn khoăn rằng các lớp học trực tuyến có thể bao gồm đa phần những bạn học sinh không đủ điều kiện kinh tế để chi trả cho lớp học truyền thống, hoặc, bạn không cần phải lo lắng rằng học sinh từ các nhóm can thiệp khác nhau thì khác biệt về mọi mặt ngoại trừ việc chúng có được nhận can thiệp hay không. Về mặt thiết kế, thử nghiệm ngẫu nhiên được tạo ra để xoá bỏ những khác biệt trên.

Chính vì lẽ đó, một kiểm định giả thiết tốt cho thử nghiệm ngẫu nhiên (kiểm tra xem dữ liệu được sử dụng có phù hợp không) là kiểm chứng liệu nhóm được can thiệp có tương tự nhóm đối chứng khi xem xét các biến số trước khi diễn ra can thiệp hay không. Trong dữ liệu trên, ta có thông tin về giới tính và sắc tộc, vì vậy ta có thể dễ dàng nhận biết nếu giữa các nhóm có sự tương đồng. Đối với các biến `gender`, `asian`, `hispanic` và `white`, ta có thể nói rằng chúng trông khá giống nhau. Tuy nhiên, biến `black` lại có sự khác biệt một chút giữa các nhóm. Điều này làm ta chú ý đến những vấn đề có thể xảy ra đối với một tập dữ liệu nhỏ. Kể cả khi có thử nghiệm ngẫu nhiên, một nhóm cũng có khả năng khác với nhóm còn lại. Trong các mẫu lớn, sự khác biệt này có xu hướng bị triệt tiêu. 

## Thử Nghiệm Lý Tưởng

Các thử nghiệm đối chứng ngẫu nhiên là cách tiếp cận đáng tin cậy nhất để thu được tác động nhân quả. Nó là một kỹ thuật đơn giản đến khó tin và thuyết phục một cách phi lý. Phương pháp này mạnh đến nỗi hầu như mọi quốc gia đều dùng nó như một bước bắt buộc để chứng minh cho sự hiệu quả của một loại thuốc mới. Trong một so sánh thú vị, các bạn có thể tưởng tượng RCT là Aang, và các phương pháp khác là Sokka, các nhân vật trong bộ phim hoạt hình Thế Thần: Tiết khí sư cuối cùng. Sokka rất ngầu và có thể thực hiện khéo léo được một vài thủ thuật này nọ, nhưng Aang có thể bẻ cong cả bốn yếu tố và kết nối được với thế giới tâm linh. Hãy nghĩ theo hướng này, nếu chúng ta có thể, RCT sẽ là tất cả những gì chúng ta sẽ làm để khám phá quan hệ nhân quả. Một RCT được thiết kế tốt là ước mơ của bất kỳ nhà khoa học nào.

![image-center](/assets/images/pythoncausal/rct/science_dream.png){: .align-center}

Đáng tiếc là phương pháp này thường rất tốn kém hoặc chỉ đơn thuần là phi đạo đức. Đôi khi, chỉ đơn giản là chúng ta không thể kiểm soát được cơ chế chỉ định. Hãy tưởng tượng bạn là một bác sĩ đang cố gắng ước tính ảnh hưởng của việc hút thuốc trong thời kỳ mang thai đến cân nặng của trẻ sơ sinh. Bạn không thể chỉ đơn giản ép buộc một nhóm ngẫu nhiên các bà mẹ hút thuốc khi mang thai. Trong một trường hợp khác, giả sử bạn làm việc cho một ngân hàng lớn và bạn cần ước tính tác động của hạn mức tín dụng đối với tỷ lệ khách hàng chấm dứt sử dụng dịch vụ của ngân hàng. Sẽ là quá tốn kém để cung cấp các hạn mức tín dụng ngẫu nhiên cho khách hàng của bạn. Hoặc khi bạn muốn hiểu tác động của việc tăng lương tối thiểu đối với tỷ lệ thất nghiệp, bạn không thể chỉ đơn giản gán một mức lương tối thiểu cho quốc gia này hay gán một mức lương tối thiểu khác cho quốc gia khác. Bạn hiểu ý tôi rồi đấy.

Một lúc nào đó, chúng ta sẽ tìm hiểu cách giảm thiểu chi phí cho thử nghiệm ngẫu nhiên bằng cách áp dụng ngẫu nhiên có điều kiện, tuy vậy chúng ta cũng không thể làm gì hơn đối với các thí nghiệm mang tính phi đạo đức hoặc bất khả thi. Tuy nhiên, bất cứ khi nào chúng ta giải quyết các câu hỏi về nhân quả, **thử nghiệm lý tưởng** rất đáng để cân nhắc. Nếu có thể, hãy luôn tự vấn bản thân rằng **thử nghiệm lý tưởng mà bạn thực hiện để khám phá ra tác động nhân quả này là gì?** Câu hỏi này có xu hướng làm sáng tỏ cách mà chúng ta có thể khám phá ra tác động nhân quả ngay cả khi không có thử nghiệm lý tưởng.

## Cơ Chế Chỉ Định

Trong thử nghiệm đối chứng ngẫu nhiên, cơ chế để chỉ định một cá thể cho một sự can thiệp này hoặc sự can thiệp khác là ngẫu nhiên. Như chúng ta sẽ thấy ở phần sau, tất cả các phương pháp suy luận nhân quả bằng cách nào đó sẽ cố gắng xác định cơ chế chỉ định của các sự can thiệp. Khi chúng ta biết chắc chắn cơ chế này hoạt động như thế nào, suy luận nhân quả sẽ chắc chắn hơn nhiều, ngay cả khi cơ chế chỉ định không phải là ngẫu nhiên.

Thật không may, không thể xác định cơ chế chỉ định chỉ đơn giản bằng cách nhìn vào dữ liệu. Ví dụ, nếu bạn có một tập dữ liệu trong đó giáo dục đại học tương quan với sự giàu có, bạn không thể biết chắc chắn được yếu tố nào gây ra yếu tố nào bằng cách chỉ nhìn vào dữ liệu. Bạn sẽ phải sử dụng kiến thức của mình về cách thế giới vận hành để lập luận cho một cơ chế chỉ định hợp lý: liệu có phải là trường hợp trong đó trường học giáo dục con người, khiến họ có năng suất lao động cao hơn và do đó họ được trả lương cao hơn. Mặt khác, nếu bạn có cái nhìn bi quan về giáo dục, bạn có thể nói rằng trường học không làm gia tăng năng suất lao động mà đây chỉ là một mối tương quan giả tạo bởi vì chỉ những gia đình giàu có mới đủ khả năng để con cái có được bằng cấp cao.

Trong các câu hỏi nhân quả, chúng ta thường có khả năng tranh luận theo cả hai cách: biến X gây ra biến Y, hoặc một biến Z thứ ba gây ra cả X và Y, và do đó mối tương quan giữa X và Y chỉ là giả. Vì lý do này mà việc biết cơ chế chỉ định cho ta một câu trả lời về nhân quả thuyết phục hơn nhiều. Đây cũng là điều làm cho suy luận nhân quả trở nên thú vị. Trong khi ứng dụng ML thường chỉ yêu cầu việc nhập các câu lệnh theo đúng thứ tự, thì việc ứng dụng suy luận nhân quả đòi hỏi bạn phải suy nghĩ nghiêm túc về cơ chế tạo ra dữ liệu đó.

## Ý tưởng chủ đạo

Chúng ta đã xem xét việc bằng cách nào mà các thử nghiệm đối chứng ngẫu nhiên là cách đơn giản và hiệu quả nhất để khám phá tác động nhân quả. Điều này được thực hiện bằng cách làm cho nhóm can thiệp và nhóm đối chứng trở nên tương đồng. Thật không may, chúng ta không thể thực hiện thử nghiệm đối chứng ngẫu nhiên vào mọi lúc, nhưng nó vẫn hữu ích nếu ta có thể biết được thử nghiệm lý tưởng mà chúng ta sẽ làm là gì.

Nếu bạn đã quen thuộc với kiến thức về thống kê, bạn  có thể phản đối ngay lúc này rằng chúng tôi đã không xem xét phương sai cho ước lượng của tác động nhân quả. Làm thế nào mà chúng tôi có thể biết rằng việc giảm 4,91 điểm không phải là do ngẫu nhiên? Nói cách khác, làm thế nào chúng tôi có thể biết được liệu sự khác biệt có ý nghĩa thống kê hay không? Và bạn có thể đúng. Đừng lo. Tiếp theo, chúng tôi sẽ ôn lại một số khái niệm trong chương tiếp theo.

## Tài liệu tham khảo

Tôi muốn dành loạt bài viết này để vinh danh Joshua Angrist, Alberto Abadie and Christopher Walters vì khóa học Kinh tế lượng tuyệt cú mèo của họ. Phần lớn ý tưởng trong loạt bài này được lấy từ các bài giảng của họ được tổ chức bởi Hiệp hội Kinh tế Mĩ.  Theo dõi các bài giảng này là những gì tôi làm trong suốt năm 2020 khó nhằn.
* [Kinh tế lượng với dữ liệu chéo](https://www.aeaweb.org/conference/cont-ed/2017-webcasts)
* [Luyện chưởng Kinh tế lượng Gần như Vô hại](https://www.aeaweb.org/conference/cont-ed/2020-webcasts)

Tôi cũng muốn giới thiệu cuốn sách lý thú của Angrist. Chúng cho tôi thấy Kinh tế lượng, hoặc 'Lượng theo cách họ gọi không chỉ vô cùng hữu ích mà còn rất vui.

* [Kinh tế lượng Gần như Vô hại](https://www.mostlyharmlesseconometrics.com/)
* [Luyện chưởng 'Lượng'](https://www.masteringmetrics.com/)

Tài liệu tham khảo cuối cùng của tôi là cuốn sách của Miguel Hernan and Jamie Robins. Nó là người bạn đồng hành tin cậy với tôi khi trả lời những câu hỏi nhân quả khó nhằn.

* [Sách Suy Luận Nhân Quả](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/)

Dữ liệu sử dụng trong phần này được trích từ một nghiên cứu của Alpert, William T., Kenneth A. Couch, và Oskar R. Harmon. 2016. ["A Randomized Assessment of Online Learning"](https://www.aeaweb.org/articles?id=10.1257/aer.p20161057). American Economic Review, 106 (5): 378-82.

![image-center](/assets/images/pythoncausal/poetry.png){: .align-center}

## Bảng Từ Viết tắt 

|Viết tắt| Tiếng Anh | Tiếng Việt |
| --- | --- | --- | 
|RCT|Randomized Controlled Trial|Thử nghiệm Ngẫu nhiên Đối chứng| 


## Bảng Thuật ngữ 

| Thuật ngữ | Tiếng Anh |
| --- | --- | 
|cơ chế chỉ định|assignment mechanism| 
|kinh tế lượng|econometrics| 
|kiểm định giả thiết|sanity check| 
|kết quả giả tưởng|counterfactual outcome| 
|kết quả tiềm năng|potential outcome| 
|mẫu|sample| 
|ngẫu nhiên có điều kiện|conditional randomisation| 
|nhóm can thiệp|treated group| 
|nhóm đối chứng|control group, untreated group| 
|phương sai|variance| 
|quan hệ nhân quả|causality, causation, causal relationship| 
|quan hệ tương quan|association, correlation| 
|suy luận nhân quả|causal inference, causal reasoning| 
|thiên lệch|bias| 
|thiên lệch dương|positive bias| 
|thử nghiệm ngẫu nhiên|randomised trial| 
|tổng thể|population| 
|ý nghĩa thống kê|statistical significance| 
|được can thiệp|treated| 
|đối chứng|untreated, non-treated| 

