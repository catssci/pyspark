# VectorAssembler

VectorAssembler는 Spark ML의 기능 중 하나로, 여러 개의 열을 선택하여 하나의 벡터 열로 조합하는 데 사용됩니다.   
이를 통해 머신러닝 알고리즘에 입력으로 사용하기 쉽게 데이터를 변환할 수 있습니다.

</aside>

```python
from pyspark.ml.feature import VectorAssembler
from pyspark.sql import SparkSession

# SparkSession 생성
spark = SparkSession.builder.getOrCreate()

# 데이터프레임 생성
data = spark.createDataFrame([
    (1, 10, 3),
    (2, 5, 8),
    (3, 7, 2)
], ['id', 'feature1', 'feature2'])

# VectorAssembler를 사용하여 열 조합
assembler = VectorAssembler(
    inputCols=['feature1', 'feature2'],  # 조합할 열들
    outputCol='features'  # 조합된 벡터 열의 이름
)

output = assembler.transform(data)

# 결과 출력
output.show()
```

```python
+---+--------+--------+----------+
| id|feature1|feature2| features |
+---+--------+--------+----------+
|  1|      10|       3|[10.0,3.0]|
|  2|       5|       8| [5.0,8.0]|
|  3|       7|       2| [7.0,2.0]|
+---+--------+--------+----------+
```
