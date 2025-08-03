# Pandas DataFrame
## Pandas
- 파이썬의 데이터 분석 라이브러리 중 하나로 데이터의 조작, 정제, 분석, 시각화 등을 위한 다양한 기능을 제공하는 라이브러리이다. 
- 판다스는 DataFrame이라는 객체로 2차원 데이터를 다루는데 `pandas.DataFrame(2차원 배열)`로 만들 수 있다. 또는 csv파일을 바로 읽어와서 데이터프레임으로 만들 수도 있다. `pandas.read_csv('.csv파일')`
- 여기서 2차원 배열로 df를 만들 때는 파이썬 리스트를 사용해도 되지만 numpy라는 라이브러리를 이용해서 만들면 좀더 편하다. 하지만 이때 numpy_arr를 슬라이싱 해서 넣을 경우 행과 열을 [][]로 슬라이싱 하는것이 아니라 [,]형태로 슬라이싱을 해야 한다.
```python
import pandas as pd

df1 = pd.DataFrame(data[:][:5])
df2 = pd.DataFrame(data[:, :5])
df1
df2
>> df1은 전체 열이 5행까지만 출력됨 # 잘못된 출력
>> df2는 전체 행이 5열까지 슬라이싱 되어 출력됨 #원하던 출력
```

- 만들어진 데이터프레임 객체에는 데이터 타입이 존재하는데 대부분 여러 형태의 데이터가 섞여 있으므로 string으로 읽은뒤 이를 의미있는 데이터 타입으로 변환하는데 이때 `astyped(Data type)`으로 int나 float, str으로 변환이 가능하다. 날짜 데이터는 `to_datetime(Data)`로 str에서 datetime으로 변환이 가능하다. 
```python
df['Date'] = pd.to_datetime(df['Date'])
df['Open'] = df['Open'].astype(float)
df['High'] = df['High'].astype(float)
df['Low'] = df['Low'].astype(float)
df['Close'] = df['Close'].astype(float)
df.info()

>> 
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1009 entries, 0 to 1008
Data columns (total 5 columns):
 #   Column  Non-Null Count  Dtype         
---  ------  --------------  -----         
 0   Date    1009 non-null   datetime64[ns]
 1   Open    1009 non-null   float64       
 2   High    1009 non-null   float64       
 3   Low     1009 non-null   float64       
 4   Close   1009 non-null   float64       
dtypes: datetime64[ns](1), float64(4)
memory usage: 39.5 KB
```
- 만약 데이터를 조건에 따라 필터링 하고 싶다면 데이터프레임을 슬라이싱 할 때 다음과 같이 조건을 넣으면 필터링이 가능하다. 
- 위의 데이터에서 날짜가 2021년 이후의 자료만 추출하고 싶다면 
```python
df_after_2021 = df[df['Date'] >= '2021-01-01']
```
- 이렇게 하면 `df_after_2021`이라는 데이터프레임에 `df`의 `Date`열의 값들 중 `2021-01-01`보다 큰 값들만 `df_after_2021`에 포함되게 된다.
- 데이터프레임의 또다른 특징은 위와같이 슬라이싱을 열의 이름으로 할 수 있다는 점이다. 직접 인덱스를 통한 슬라이싱도 가능하지만 'Date'와 같은 열 이름으로 해당 열 전체를 가져올 수 있다. 단 이름을 통한 슬라이싱은 단일 열에만 적용이 가능하고 ['Date', 'Cloase']나 ['Open':'Close']와 같이 여러 열에 대한 슬라이싱은 불가능하다.