# 2주차 

# <01. 파이썬 기반의 머신러닝과 생태계 이해(11~19)>

## 01-11. 판다스 개요와 기본 API-01

### 판다스(Pandas)

- 파이썬에서 데이터 처리를 위해 존재하는 가장 인기 있는 라이브러리
- 일반적으로 대부분의 데이터 세트는 2차원 데이터(즉, RowxColumn으로 구성되어 있음)
- 2차원 데이터가 인기 있는 이유는 인간이 가장 이해하기 쉬운 데이터 구조이면서 효과적으로 데이터를 담을 수 있기 때문
- 판다스는 2차원 데이터를 효율적으로 가공 및 처리할 수 있는 다양하고 훌륭한 기능을 제공
- 또한 시계열 데이터에 매우 편리한 기능을 제공함

### 판다스의 주요 구성 요소 - DataFram, Series, Index

![image-20201109213156915](/Users/mac/Library/Application Support/typora-user-images/image-20201109213156915.png)

### 기본 API

1. read_csv() : csv파일을 DataFrame으로 로딩, sep인자를 콤마가 아닌 다른 분리자로 변경하여 다른 유형의 파일 로드도 가능
2. head() : DataFrame의 맨 앞 일부 데이터만 추출
3. shape : DataFrame의 행과 열의 크기를 가지고 있는 속성
4. info() : DataFrame내의 컬럼명, 데이터 타입, 널 건수, 데이터 건수 정보를 제공
5. describe() : 데이터값들의 평균, 표준편차, 4분위 분포도를 제공(숫자형 컬럼들에 대해서 해당 정보를 제공)
6. value_counts() : 동일한 개별 데이터 값이 몇 건 있는지 제공(즉, 개별 데이터 값의 분포도 제공)
   * 단, 해당 함수는 Series객체에서만 호출 될 수 있으므로 반드시 DataFrame을 Series로 변환한 뒤 호출
7. sort_values() : by=정렬컬럼, ascending=True 또는 False로 오름차순/내림차순으로 정렬

-> 실습





## 01-12. 판다스 개요와 기본 API-02

-> 01-11. 이어서 실습



## 01-13. 판다스 DataFrame의 변환, 컬럼 세트 생성/수정, 삭제 및 Index 객체 소개

### DataFrame과 리스트, 딕셔너리, 넘파이, ndarray 상호 변환

![image-20201110125204607](/Users/mac/Library/Application Support/typora-user-images/image-20201110125204607.png)

### DataFrame의 drop()

![image-20201110130458948](/Users/mac/Library/Application Support/typora-user-images/image-20201110130458948.png)

- axis: DataFrame의 로우를 삭제할 때는 axis=0, 컬럼을 삭제할 때는 axis=1로 설정
- 원본 DataFrame은 유지하고 드롭된 DataFrame을 새롭게 객체 변수로 받고 싶다면 inplace=False로 설정(디폴트 값이 False임)
- 원본 DataFrame에 드롭된 결과를 적용할 경우에는 inplace=True를 적용
-  원본 DataFrame에서 드롭된 DataFrame을 다시 원본 DataFrame 객체 변수로 할당하면 원본 DataFrame에 드롭된 결과를 적용할 경우와 같음(단, 기존 원본 DataFrame 객체 변수는 메모리에서 추후 제거됨)

### Index

- 판다스의 인덱스 객체는 RDBMS의 PK(Primary Key)와 유사하게 DataFrame, Series의 레코드를 고유하게 식별하는 객체임
- DataFrame, Series에서 인덱스 객체만 추출하려면 DataFrame.index 또는 Series.index 속성을 통해서 가능
- Series객체는 인덱스 객체를 포함하지만 Series 객체에 연산 함수를 적용할 때 인덱스는 연산에서 제외
  - 이 경우 인덱스는 오직 식별용으로만 사용
- DataFrame 및 Series에 reset_index() 메서드를 수행하면 새롭게 인덱스를 연속 숫자 형으로 할당하며 기존 인덱스는 'index'라는 새로운 컬럼 명으로 추가함

-> 실습

## 01-14.  판다스 데이터 셀렉션과 필터링 - 01

### 데이터 셀렉션 및 필터링

1. [ ] : bracket 
   - 컬럼 기반 필터링 또는 불린 인덱싱 필터링 제공
2. ix[], loc[], iloc[]
   - 명칭/위치 기반 인덱싱을 제공
3. **boolean indexing**
   - 조건식에 따른 필터링 제공

### 데이터 셀렉션 및 필터링 - ix, loc, iloc

- 명칭(Lable)기반 인덱싱을 컬럼의 명칭을 기반으로 위치를 지정하는 방식으로 '컬럼 명'같이 명칭으로 열 위치를 지정함

- 위치(Position)기반 인덱싱을 0을 출발점으로 하는 가로축, 세로축 좌표 기반의 행과 열 위치를 기반으로 데이터를 지정

  - **따라서 행, 열 위치 값으로 정수가 입력됨**

  ![image-20201110133313212](/Users/mac/Library/Application Support/typora-user-images/image-20201110133313212.png)

### 명칭 기반과 위치 기반 인덱싱 구분

![image-20201110133504790](/Users/mac/Library/Application Support/typora-user-images/image-20201110133504790.png)

- 주의 ix[0,1]은 오류를 일으킴
  - RangeIndex의 0인지 위치 0인지 구분을 할 수 없기 때문 

### 불린 인덱싱

위치 기반, 명칭 기반 인덱싱 모두 사용할 필요 없이 조건식을 []안에 기입하여 간편하게 필터링을 수행

예:) titanic_boolean = titanic_df[titanic_df['Age'] > 60]



## 01-15. 판다스 데이터 셀렉션과 필터링 - 02


## 01-16. 판다스 Aggregation 함수와 Group by 수행



## 01-17. 판다스 결손 데이터 처리하기

## 01-18. 판다스 람다식 적용하여 데이터 가공하기

## 01-19. 파이썬 기반의 머신러닝과 생태계 이해 Summary







































