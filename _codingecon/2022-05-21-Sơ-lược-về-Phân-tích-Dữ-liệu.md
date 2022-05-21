---
layout: single
title: Sơ lược về Phân tích Dữ liệu
excerpt: 
permalink: /codingecon/ce01
categories:
  - series coding cho kinh tế học
tags:
  - economics
  - python
  - data
sidebar:
    nav: codingecon
author_profile: true
---



Trước khi bắt đầu, các bạn có thể cài đặt Python và các packages phục vụ cho việc phân tích dữ liệu một cách dễ dàng thông qua Anaconda tại đây https://www.anaconda.com/products/distribution

# Nạp và kiểm tra kiểu dữ liệu

Việc nạp dữ liệu vào khung dữ liệu được thực hiện bằng các lệnh như df = pd.read_csv (...) hoặc df = pd.read_stata (...). Chúng ta sẽ nạp dữ liệu về Chiến tranh giữa các vì sao:


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from pathlib import Path


# Đặt hạt giống nhằm thuận tiện cho việc tái tạo dãy số ngẫu nhiên
np.random.seed(10)
# Cài đặt số dòng hiển thị tối đa
pd.set_option("display.max_rows", 6)
# Cài đặt plot
plt.style.use(
    "https://github.com/aeturrell/coding-for-economists/raw/main/plot_style.txt"
)

df = (pd.read_csv(
    "https://github.com/aeturrell/coding-for-economists/raw/main/data/starwars.csv",
    index_col=0,
    )
    .dropna(subset=["species"])
    )
# Kiểm tra thông tin về khung dữ liệu
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 82 entries, 0 to 86
    Data columns (total 8 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   name        82 non-null     object 
     1   height      77 non-null     float64
     2   mass        58 non-null     float64
     3   hair_color  77 non-null     object 
     4   eye_color   80 non-null     object 
     5   gender      79 non-null     object 
     6   homeworld   74 non-null     object 
     7   species     82 non-null     object 
    dtypes: float64(2), object(6)
    memory usage: 5.8+ KB


# Hiển thị một vài dòng đầu tiên với head()


```python
df.head()

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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luke Skywalker</td>
      <td>172.0</td>
      <td>77.0</td>
      <td>blond</td>
      <td>blue</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C-3PO</td>
      <td>167.0</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>yellow</td>
      <td>NaN</td>
      <td>Tatooine</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
      <td>Naboo</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Darth Vader</td>
      <td>202.0</td>
      <td>136.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Leia Organa</td>
      <td>150.0</td>
      <td>49.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>female</td>
      <td>Alderaan</td>
      <td>Human</td>
    </tr>
  </tbody>
</table>
</div>



# Lọc các dòng và cột theo điều kiện bằng cách sử dụng lệnh df.loc [điều kiện hoặc dòng, cột]

.loc là viết tắt của location (vị trí) và cho phép người dùng lọc (còn gọi là tập hợp con) một khung dữ liệu. .loc hoạt động giống như một chỉ số, vì vậy nó luôn đi kèm với dấu ngoặc vuông, ví dụ: df.loc [...].

loc cần hai tham số đầu vào. Đầu tiên là danh sách tên của các dòng bạn muốn chọn hoặc một điều kiện (tức là giá trị logic, với 1= đúng, 0=sai, có cùng độ dài với khung dữ liệu) chọn các dòng nhất định. Hãy nhớ rằng, bạn có thể dễ dàng tạo một loạt các giá trị logic bằng cách kiểm tra một cột với một điều kiện, ví dụ: df ['column1'] == 'black'.

Tham số thứ hai bao gồm danh sách tên cột bạn muốn chọn. Trong cả hai trường hợp,: là viết tắt của "sử dụng tất cả các dòng" hoặc "sử dụng tất cả các cột". Nếu bạn có (các) điều kiện hoặc (các) cột (nhưng không phải cả hai), bạn chỉ cần viết df [condition (s)] hoặc df [column (s)].

Dưới đây là một ví dụ với một điều kiện được tạo từ hai phép so sánh và danh sách các cột:


```python
df.loc[(df["hair_color"] == "brown") & (df["eye_color"] == "blue"), ["name", "species"]]
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
      <th>name</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>Beru Whitesun lars</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chewbacca</td>
      <td>Wookiee</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Jek Tono Porkins</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Qui-Gon Jinn</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Cliegg Lars</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Tarfful</td>
      <td>Wookiee</td>
    </tr>
  </tbody>
</table>
</div>



# Sắp xếp dòng với lệnh .sort_values()

Sằp xếp theo thứ tự giảm dần bằng lệnh sort_values(columns, ascending=False)


```python
df.sort_values(["height", "mass"])
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18</th>
      <td>Yoda</td>
      <td>66.0</td>
      <td>17.0</td>
      <td>white</td>
      <td>brown</td>
      <td>male</td>
      <td>NaN</td>
      <td>Yoda's species</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Ratts Tyerell</td>
      <td>79.0</td>
      <td>15.0</td>
      <td>none</td>
      <td>NaN</td>
      <td>male</td>
      <td>Aleen Minor</td>
      <td>Aleena</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Wicket Systri Warrick</td>
      <td>88.0</td>
      <td>20.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>male</td>
      <td>Endor</td>
      <td>Ewok</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Rey</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>brown</td>
      <td>hazel</td>
      <td>female</td>
      <td>NaN</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Poe Dameron</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>brown</td>
      <td>brown</td>
      <td>male</td>
      <td>NaN</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>84</th>
      <td>BB8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>none</td>
      <td>black</td>
      <td>none</td>
      <td>NaN</td>
      <td>Droid</td>
    </tr>
  </tbody>
</table>
<p>82 rows × 8 columns</p>
</div>



# Chọn nhiều dòng hoặc cột 

Có thể dùng lát cắt để chọn nhiều dòng hoặc cột theo tên bằng cách sử dụng .loc [tên dòng đầu : tên dòng cuối : bước nhảy, tên cột đầu :tên cột cuối : bước nhảy] hoặc theo vị trí bằng cách sử dụng .iloc [chỉ số dòng đầu : chỉ số dòng cuối : bước nhảy,chỉ số cột đầu : chỉ số cột cuối : bước nhảy].

Ví dụ 1, chọn mỗi dòng thứ 10 từ hàng thứ hai và các cột giữa "tên" và "giới tính":


```python
df.loc[2::10, "name":"gender"]
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Chewbacca</td>
      <td>228.0</td>
      <td>112.0</td>
      <td>brown</td>
      <td>blue</td>
      <td>male</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bossk</td>
      <td>190.0</td>
      <td>113.0</td>
      <td>none</td>
      <td>red</td>
      <td>male</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Plo Koon</td>
      <td>188.0</td>
      <td>80.0</td>
      <td>none</td>
      <td>black</td>
      <td>male</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Bail Prestor Organa</td>
      <td>191.0</td>
      <td>NaN</td>
      <td>black</td>
      <td>brown</td>
      <td>male</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Shaak Ti</td>
      <td>178.0</td>
      <td>57.0</td>
      <td>none</td>
      <td>black</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 6 columns</p>
</div>



Lưu ý rằng với trường hợp này, loc chấp nhận số vì với tập dữ liệu này, tên dòng được định dạng số. Nếu tên dòng định dạng văn bản và ta muốn cắt các dòng theo vị trí chỉ số của chúng, ta sẽ phải sử dụng iloc.

Ví dụ 2, chọn 5 dòng đầu tiên và 2 cột cuối cùng theo vị trí chỉ số:


```python
df.iloc[:5, -2:]

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
      <th>homeworld</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tatooine</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Naboo</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alderaan</td>
      <td>Human</td>
    </tr>
  </tbody>
</table>
</div>



# Chọn ngẫu nhiên mẫu với lệnh .sample
.sample(n) chọn ngẫu nhiên n dòng, .sample (frac = 0,4) chọn 40% dữ liệu, replace = True chọn mẫu bằng thay thế

Lấy mẫu gồm 5 dòng:


```python
df.sample(5)

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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Darth Vader</td>
      <td>202.0</td>
      <td>136.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Dud Bolt</td>
      <td>94.0</td>
      <td>45.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Vulpter</td>
      <td>Vulptereen</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Darth Maul</td>
      <td>175.0</td>
      <td>80.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Dathomir</td>
      <td>Zabrak</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Sebulba</td>
      <td>112.0</td>
      <td>40.0</td>
      <td>none</td>
      <td>orange</td>
      <td>male</td>
      <td>Malastare</td>
      <td>Dug</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Mon Mothma</td>
      <td>150.0</td>
      <td>NaN</td>
      <td>auburn</td>
      <td>blue</td>
      <td>female</td>
      <td>Chandrila</td>
      <td>Human</td>
    </tr>
  </tbody>
</table>
</div>



# Đổi tên bằng .rename
Bạn có thể đổi tên tất cả các cột bằng lệnh df.rename (columns = str.lower) để đặt tất cả các cột ở dạng chữ thường. Ngoài ra, sử dụng từ điển để cho biết cột nào nên thay thế bằng tên gì:


```python
df.rename(columns={"homeworld": "home_world"})
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>home_world</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luke Skywalker</td>
      <td>172.0</td>
      <td>77.0</td>
      <td>blond</td>
      <td>blue</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C-3PO</td>
      <td>167.0</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>yellow</td>
      <td>NaN</td>
      <td>Tatooine</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
      <td>Naboo</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Poe Dameron</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>brown</td>
      <td>brown</td>
      <td>male</td>
      <td>NaN</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>84</th>
      <td>BB8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>none</td>
      <td>black</td>
      <td>none</td>
      <td>NaN</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Padmé Amidala</td>
      <td>165.0</td>
      <td>45.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>female</td>
      <td>Naboo</td>
      <td>Human</td>
    </tr>
  </tbody>
</table>
<p>82 rows × 8 columns</p>
</div>



# Thêm các cột mới với .assign hoặc assignment
Thông thường, bạn sẽ muốn tạo các cột mới dựa trên các cột hiện có.

Có hai cách để làm điều này. Hãy cùng xem cả hai với một ví dụ trong đó chúng tôi muốn tạo một cột chiều cao mới tính bằng mét, được gọi là "height_m:.

Cách đầu tiên, và được sử dụng phổ biến nhất, được gọi là phép gán giá trị và chỉ bao gồm việc nhập tên cột mới trong khung dữ liệu và đặt nó ở phía bên trái của biểu thức gán được tính dựa trên các cột khung dữ liệu hiện có ở phía bên phải . Ví dụ: df ['height_m'] = df ['height'] / 100.

Thứ hai là sử dụng phương thức gán trực tiếp trên khung dữ liệu. Trong trường hợp này, câu lệnh gán xuất hiện bên trong dấu ngoặc. Ví dụ, df.assign (height_m = df ["height"] / 100).

Hãy xem các ví dụ của cả hai phương pháp gán giá trị này.

Trước tiên, hãy sử dụng phương pháp đầu tiên:


```python
df['height_m'] = df['height']/100
df.head()
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
      <th>height_m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luke Skywalker</td>
      <td>172.0</td>
      <td>77.0</td>
      <td>blond</td>
      <td>blue</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>1.72</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C-3PO</td>
      <td>167.0</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>yellow</td>
      <td>NaN</td>
      <td>Tatooine</td>
      <td>Droid</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
      <td>Naboo</td>
      <td>Droid</td>
      <td>0.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Darth Vader</td>
      <td>202.0</td>
      <td>136.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>2.02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Leia Organa</td>
      <td>150.0</td>
      <td>49.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>female</td>
      <td>Alderaan</td>
      <td>Human</td>
      <td>1.50</td>
    </tr>
  </tbody>
</table>
</div>



Và bây giờ là hàm .assign


```python
df = df.assign(height_m=df["height"] / 100)
df.head()
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
      <th>height_m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luke Skywalker</td>
      <td>172.0</td>
      <td>77.0</td>
      <td>blond</td>
      <td>blue</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>1.72</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C-3PO</td>
      <td>167.0</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>yellow</td>
      <td>NaN</td>
      <td>Tatooine</td>
      <td>Droid</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
      <td>Naboo</td>
      <td>Droid</td>
      <td>0.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Darth Vader</td>
      <td>202.0</td>
      <td>136.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>2.02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Leia Organa</td>
      <td>150.0</td>
      <td>49.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>female</td>
      <td>Alderaan</td>
      <td>Human</td>
      <td>1.50</td>
    </tr>
  </tbody>
</table>
</div>



Cột mới tạo được đặt cuối cùng; tuy nhiên, chúng tôi muốn nó bên cạnh cột chiều cao bằng cách sắp xếp các cột (axis = 1) theo thứ tự bảng chữ cái:


```python
(df.assign(height_m=df["height"] / 100).sort_index(axis=1))
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
      <th>eye_color</th>
      <th>gender</th>
      <th>hair_color</th>
      <th>height</th>
      <th>height_m</th>
      <th>homeworld</th>
      <th>mass</th>
      <th>name</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>blue</td>
      <td>male</td>
      <td>blond</td>
      <td>172.0</td>
      <td>1.72</td>
      <td>Tatooine</td>
      <td>77.0</td>
      <td>Luke Skywalker</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>1</th>
      <td>yellow</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>167.0</td>
      <td>1.67</td>
      <td>Tatooine</td>
      <td>75.0</td>
      <td>C-3PO</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>2</th>
      <td>red</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>96.0</td>
      <td>0.96</td>
      <td>Naboo</td>
      <td>32.0</td>
      <td>R2-D2</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>83</th>
      <td>brown</td>
      <td>male</td>
      <td>brown</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Poe Dameron</td>
      <td>Human</td>
    </tr>
    <tr>
      <th>84</th>
      <td>black</td>
      <td>none</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BB8</td>
      <td>Droid</td>
    </tr>
    <tr>
      <th>86</th>
      <td>brown</td>
      <td>female</td>
      <td>brown</td>
      <td>165.0</td>
      <td>1.65</td>
      <td>Naboo</td>
      <td>45.0</td>
      <td>Padmé Amidala</td>
      <td>Human</td>
    </tr>
  </tbody>
</table>
<p>82 rows × 9 columns</p>
</div>



Để ghi đè các cột hiện có, chỉ cần sử dụng height = df ['height'] / 100 với phương thức gán hoặc df ['height'] = df ['height'] / 100.

# Mô tả các giá trị số với .describe ()


```python
df.describe()
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
      <th>height</th>
      <th>mass</th>
      <th>height_m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>77.000000</td>
      <td>58.000000</td>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>175.103896</td>
      <td>98.162069</td>
      <td>1.751039</td>
    </tr>
    <tr>
      <th>std</th>
      <td>34.483629</td>
      <td>170.810183</td>
      <td>0.344836</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>180.000000</td>
      <td>79.000000</td>
      <td>1.800000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>191.000000</td>
      <td>84.750000</td>
      <td>1.910000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>264.000000</td>
      <td>1358.000000</td>
      <td>2.640000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 3 columns</p>
</div>



# Nhóm các giá trị với .groupby()


```python
df.groupby("species")[["height", "mass"]].mean()
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
      <th>height</th>
      <th>mass</th>
    </tr>
    <tr>
      <th>species</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aleena</th>
      <td>79.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>Besalisk</th>
      <td>198.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>Cerean</th>
      <td>198.0</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Xexto</th>
      <td>122.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Yoda's species</th>
      <td>66.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>Zabrak</th>
      <td>173.0</td>
      <td>80.0</td>
    </tr>
  </tbody>
</table>
<p>37 rows × 2 columns</p>
</div>



# Thêm các cột đã biến đổi bằng cách sử dụng .transform () 

Thông thường, việc thêm một cột vào khung dữ liệu là kết quả của một bước trung gian giữa bước groupby() và tổng hợp. Ví dụ, trừ giá trị trung bình của nhóm. Transform thực hiện điều này và trả về một cột đã biến đổi có cùng hình dạng với khung dữ liệu ban đầu. Biến đổi bảo toàn chỉ số ban đầu. (Có những phương pháp khác, chẳng hạn như apply, trả về khung dữ liệu mới với các biến theo nhóm làm chỉ số mới.)

Dưới đây là một ví dụ về hàm transform được sử dụng để loại giá trị trung bình theo loài. Lưu ý rằng chúng ta sử dụng các hàm lambda ở đây. Các hàm lambda là một cách viết hàm nhanh chóng mà không cần đặt tên cho chúng, ví dụ: lambda x: x + 1 xác định một hàm thêm một vào x. Trong ví dụ dưới đây, x trong hàm lambda đảm nhận vai trò của khối lượng được nhóm theo loài.


```python
df["mass_demean_species"] = df.groupby("species")["mass"].transform(lambda x: x - x.mean())
df.head()
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
      <th>name</th>
      <th>height</th>
      <th>mass</th>
      <th>hair_color</th>
      <th>eye_color</th>
      <th>gender</th>
      <th>homeworld</th>
      <th>species</th>
      <th>height_m</th>
      <th>mass_demean_species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Luke Skywalker</td>
      <td>172.0</td>
      <td>77.0</td>
      <td>blond</td>
      <td>blue</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>1.72</td>
      <td>-5.781818</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C-3PO</td>
      <td>167.0</td>
      <td>75.0</td>
      <td>NaN</td>
      <td>yellow</td>
      <td>NaN</td>
      <td>Tatooine</td>
      <td>Droid</td>
      <td>1.67</td>
      <td>5.250000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>R2-D2</td>
      <td>96.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>red</td>
      <td>NaN</td>
      <td>Naboo</td>
      <td>Droid</td>
      <td>0.96</td>
      <td>-37.750000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Darth Vader</td>
      <td>202.0</td>
      <td>136.0</td>
      <td>none</td>
      <td>yellow</td>
      <td>male</td>
      <td>Tatooine</td>
      <td>Human</td>
      <td>2.02</td>
      <td>53.218182</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Leia Organa</td>
      <td>150.0</td>
      <td>49.0</td>
      <td>brown</td>
      <td>brown</td>
      <td>female</td>
      <td>Alderaan</td>
      <td>Human</td>
      <td>1.50</td>
      <td>-33.781818</td>
    </tr>
  </tbody>
</table>
</div>



# Lập biểu đồ nhanh với .plot.

Bao gồm biểu đồ phân tán biểu, diện tích, cột, hộp, mật độ, lục giác, histogram, kernel và đường.


```python
df.plot.scatter("mass", "height", alpha=0.5);
```


![png](output_35_0.png)



```python
df.plot.box("species");
```


![png](output_36_0.png)



```python
df["height"].plot.kde(bw_method=0.3);

```


![png](output_37_0.png)


# Xuất kết quả và thống kê mô tả

Ta có thể xuất kết quả sang tệp latex để tích hợp vào bài báo, bản trình bày hoặc áp phích. Giả sử chúng ta đã có một số thống kê mô tả trên khung dữ liệu:


```python
table = df[["mass", "height"]].agg([np.mean, np.std])
table
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
      <th>mass</th>
      <th>height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>98.162069</td>
      <td>175.103896</td>
    </tr>
    <tr>
      <th>std</th>
      <td>170.810183</td>
      <td>34.483629</td>
    </tr>
  </tbody>
</table>
</div>



Ta có thể xuất tệp này sang nhiều định dạng, bao gồm chuỗi, html, xml, markdown, clipboard, Excel, v.v.

Đây là một ví dụ về việc xuất bảng gấu trúc của bạn sang bảng LaTeX:


```python
print(table.to_latex(caption="A Table", label="tab:descriptive"))
```

    \begin{table}
    \centering
    \caption{A Table}
    \label{tab:descriptive}
    \begin{tabular}{lrr}
    \toprule
    {} &        mass &      height \\
    \midrule
    mean &   98.162069 &  175.103896 \\
    std  &  170.810183 &   34.483629 \\
    \bottomrule
    \end{tabular}
    \end{table}
    


Việc ghi vào terminal không hữu ích cho việc hoàn thành bài báo hoặc báo cáo! Để xuất dưới dạng tệp, hãy sử dụng table.to_latex('file.tex', ...).
