# Pandas
* Pandas에서는 1차원 데이터를 Series로, 2차원 데이터를 DataFrame으로 다룸.
  
### Series
* Series는 리스트와 비슷하지만, 인덱스에 이름을 붙여 지정해줄 수 있다.
* Series는 인덱스가 같은 다른 Series와 + 연산이 가능하다. (이 경우엔 각각 일치하는 인덱스에 해당하는 값끼리 더해진다.)
* 사용 예
```py
from pandas import Series, DataFrame

kakao = Series([92600, 92400, 92100], index=['2016-02-19', '2016-02-18', '2016-02-17'])
print(kakao)
```
```
2016-02-19    92600
2016-02-18    92400
2016-02-17    92100
dtype: int64
```

### DataFrame
* DataFrame은 인덱스가 같은 여러 개의 Series 객체로 구성된 자료구조와 같다.

* 사용 예
```py
from pandas import Series, DataFrame

raw_data = {'col2' : [1, 2, 3, 4],
            'col0' : [5, 6, 7, 8],
            'col1' : [9, 10, 11, 12]}

data = DataFrame(raw_data, columns=['col0', 'col1', 'col2'], index=['a', 'b', 'c', 'd'])
print(data)
```
```
   col0  col1  col2
a     5     9     1
b     6    10     2
c     7    11     3
d     8    12     4
```

## Pandas-datareader
* 데이터를 읽어오는 데 사용하는 서브 패키지