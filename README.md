# BÀI TẬP THỰC HÀNH 5.4 SWISSCODING
***
### 1. **YÊU CẦU BÀI THỰC HÀNH**

Đường dẫn phía sau chứa các yêu cầu bài thực hành :  [LINK THỰC HÀNH]([https://colab.research.google.com/drive/1TpyZNqmoa2y_kmNK8Osj3fIrc6iqtkil?usp=sharing](https://github.com/haduy2009sg/Swisscoding_5.4/blob/main/Duy_%5Btemplate%5D_Restaurant_tips_analysis.ipynb)) 
<p> *NOTE: Nhớ rằng chọn chia sẻ bài tập nha (https://github.com/haduy2009sg/Swisscoding_5.4/blob/main/image.png) </p>

### 2. **NHỮNG CÁI NHÌN ĐẦU TIÊN VỀ DỮ LIỆU**
##### Tôi thêm dữ liệu:

 ```python
 import data and data info
 import pandas as pd
 import matplotlib.pyplot as plt
 df = pd.read_csv("https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv")
 display(df.head())
 df.info()
```

 Tôi được thông tin dưới đây:

|    |   id |   total_bill |   tip | sex    | smoker   | day   | time   |   size |
|---:|-----:|-------------:|------:|:-------|:---------|:------|:-------|-------:|
|  0 |    0 |        16.99 |  1.01 | Female | No       | Sun   | Dinner |      2 |
|  1 |    1 |        10.34 |  1.66 | Male   | No       | Sun   | Dinner |      3 |
|  2 |    2 |        21.01 |  3.5  | Male   | No       | Sun   | Dinner |      3 |
|  3 |    3 |        23.68 |  3.31 | Male   | No       | Sun   | Dinner |      2 |
|  4 |    4 |        24.59 |  3.61 | Female | No       | Sun   | Dinner |      4 |
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 244 entries, 0 to 243
Data columns (total 8 columns):
    Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   id          244 non-null    int64  
 1   total_bill  244 non-null    float64
 2   tip         244 non-null    float64
 3   sex         244 non-null    object 
 4   smoker      244 non-null    object 
 5   day         244 non-null    object 
 6   time        244 non-null    object 
 7   size        244 non-null    int64  
dtypes: float64(2), int64(2), object(4)
memory usage: 15.4+ KB
```

##### Tôi thay đổi datatype 'object' của một số cột:

```python
df = df.convert_dtypes()
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 244 entries, 0 to 243
Data columns (total 8 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   id          244 non-null    Int64  
 1   total_bill  244 non-null    Float64
 2   tip         244 non-null    Float64
 3   sex         244 non-null    string 
 4   smoker      244 non-null    string 
 5   day         244 non-null    string 
 6   time        244 non-null    string 
 7   size        244 non-null    Int64  
dtypes: Float64(2), Int64(2), string(4)
memory usage: 16.3 KB
```
##### Thống kê mô tả cơ bản:
```python
df.describe()
```
|index|id|total\_bill|tip|size|
|---|---|---|---|---|
|count|244\.0|244\.0|244\.0|244\.0|
|mean|121\.5|19\.78594262295082|2\.99827868852459|2\.569672131147541|
|std|70\.58092282385282|8\.902411954856856|1\.3836381890011822|0\.9510998047322344|
|min|0\.0|3\.07|1\.0|1\.0|
|25%|60\.75|13\.3475|2\.0|2\.0|
|50%|121\.5|17\.795|2\.9|2\.0|
|75%|182\.25|24\.127499999999998|3\.5625|3\.0|
|max|243\.0|50\.81|10\.0|6\.0|

### 3. Thông kê những yếu tố ảnh hưởng đến tiền tip

##### * Người hút thuốc và không hút thuốc
