---
layout: post
title:  "python dfply package with diamonds test blog"
date:   2018-11-02 00:10:00 +0900
categories: test
---

# dfply

정말 잘 써질 수 있을까요?
이렇게 될 수만 있다면 정말 좋겠네요. 기대 만빵!

이글은 vi를 이용해서 직접 작성하는 것입니다. 생각보다 나쁘지 않고 잘 써지는 것 같아요. 블로그 포스팅을 이렇게 할 수 있다는 것이 신기합니다. 재미도 있고요. md 파일을 이렇게 vi로 직접 편집해서 멋진 테마로 포장할 수 있다는 것이 장점인 것 같습니다.

* diamond 예제를 통햬서 확인
* https://github.com/kieferk/dfply#n


```python
from IPython.core.display import display, HTML
display(HTML("<style>.container { width:90% !important; }</style>"))
```


<style>.container { width:90% !important; }</style>

하지만, 바로 위의 이 표는 예쁘게 나오지 않는 것 같아요. 스타일 조정을 해봐야 할 것 같네요. 


```python
import pandas as pd
from pandas import Series, DataFrame
import csv

from dfply import *
from matplotlib.pyplot import *
```

## pipe operator >> and >>=

* '>>' 를 사용하여 chain 가능
* '>>=' 를 사용하면 소스 df와 결과 df를 한꺼번에 표현 가능



```python
d10 = diamonds >> head(10) 
```


```python
d10 >>= head(5)
```

## X Symbol

* pipe operation에서 변수로 사용되는 컬럼명 앞에 X를 붙임


```python
diamonds >> select(X.carat, X.cut) >> head(3)
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
      <th>carat</th>
      <th>cut</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
    </tr>
  </tbody>
</table>
</div>



## select / drop

* 아래와 같이 chain 할 때, 칸을 띄어 쓰려면 괄호를 해주어야 한다는 것
* 다른 방법이 없을까?


```python
( 
    diamonds 
    >> select(X) # select all coloumns
    >> head(5)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.29</td>
      <td>Premium</td>
      <td>I</td>
      <td>VS2</td>
      <td>62.4</td>
      <td>58.0</td>
      <td>334</td>
      <td>4.20</td>
      <td>4.23</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.31</td>
      <td>Good</td>
      <td>J</td>
      <td>SI2</td>
      <td>63.3</td>
      <td>58.0</td>
      <td>335</td>
      <td>4.34</td>
      <td>4.35</td>
      <td>2.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds 
    >> select(0,1) # column index available
    >> head(3)
)
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
      <th>carat</th>
      <th>cut</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
    >> select(0,-1, X.color, ['price']) # select column with multi grammar
    >> head(3)
)
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
      <th>carat</th>
      <th>z</th>
      <th>color</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>2.43</td>
      <td>E</td>
      <td>326</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>2.31</td>
      <td>E</td>
      <td>326</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>2.31</td>
      <td>E</td>
      <td>327</td>
    </tr>
  </tbody>
</table>
</div>



* ~ 를 사용하면 제외 컬럼 선택을 할 수 있음


```python
(
    diamonds 
    >> select(~X.cut, ~X.carat) # exclude columns
    >> head(3)
)
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
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>E</td>
      <td>VS1</td>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>



* ~ 표시는 반드시 X 앞에 있어야 함. 아래처럼 [부호 앞에 있으면 에러


```python
(
    diamonds
    >> select(~[X.color, X.clarity, X.depth]) # error4
    >> head(3)
)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-60-57c531d84c9d> in <module>()
          2     diamonds
          3     >> select(~[X.color, X.clarity, X.depth])
    ----> 4     >> head(3)
          5 )


    TypeError: bad operand type for unary ~: 'list'


* 아래와 같은 함수를 사용할 수 있음
        * starts_with(prefix): find columns that start with a string prefix.
        * ends_with(suffix): find columns that end with a string suffix.
        * contains(substr): find columns that contain a substring in their name.
        * everything(): all columns.
        * columns_between(start_col, end_col, inclusive=True): find columns between a specified start and end column. The inclusive boolean keyword argument indicates whether the end column should be included or not.
        * columns_to(end_col, inclusive=True): get columns up to a specified end column. The inclusive argument indicates whether the ending column should be included or not.
        * columns_from(start_col): get the columns starting at a specified column.


```python
(
    diamonds
#     >> select(X)
    >> select(starts_with('c'))
    >> head(3)
)
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
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
#     >> select(X)
    >> select(~starts_with('c')) # using invert symbol
    >> head(3)
)
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
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
#     >> select(X)
    >> select(columns_from(X.price))
    >> head(3)
)
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
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
#     >> select(X)
    >> select(columns_to(X.price), 0, 1)
    >> head(3)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>56.9</td>
      <td>65.0</td>
    </tr>
  </tbody>
</table>
</div>



## subsetting and filtering

* row_slice()


```python
(
    diamonds 
    >> row_slice([0,3,5]) # select row index
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.29</td>
      <td>Premium</td>
      <td>I</td>
      <td>VS2</td>
      <td>62.4</td>
      <td>58.0</td>
      <td>334</td>
      <td>4.20</td>
      <td>4.23</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.24</td>
      <td>Very Good</td>
      <td>J</td>
      <td>VVS2</td>
      <td>62.8</td>
      <td>57.0</td>
      <td>336</td>
      <td>3.94</td>
      <td>3.96</td>
      <td>2.48</td>
    </tr>
  </tbody>
</table>
</div>



* row_slice()는 group_by와 함께 사용가능


```python
(
    diamonds 
    >> group_by('cut')
    >> row_slice([1,2]) # row extract by index for each group
#     >> head(3)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>91</th>
      <td>0.86</td>
      <td>Fair</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.1</td>
      <td>69.0</td>
      <td>2757</td>
      <td>6.45</td>
      <td>6.33</td>
      <td>3.52</td>
    </tr>
    <tr>
      <th>97</th>
      <td>0.96</td>
      <td>Fair</td>
      <td>F</td>
      <td>SI2</td>
      <td>66.3</td>
      <td>62.0</td>
      <td>2759</td>
      <td>6.27</td>
      <td>5.95</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.31</td>
      <td>Good</td>
      <td>J</td>
      <td>SI2</td>
      <td>63.3</td>
      <td>58.0</td>
      <td>335</td>
      <td>4.34</td>
      <td>4.35</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.30</td>
      <td>Good</td>
      <td>J</td>
      <td>SI1</td>
      <td>64.0</td>
      <td>55.0</td>
      <td>339</td>
      <td>4.25</td>
      <td>4.28</td>
      <td>2.73</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>J</td>
      <td>VS1</td>
      <td>62.8</td>
      <td>56.0</td>
      <td>340</td>
      <td>3.93</td>
      <td>3.90</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.31</td>
      <td>Ideal</td>
      <td>J</td>
      <td>SI2</td>
      <td>62.2</td>
      <td>54.0</td>
      <td>344</td>
      <td>4.35</td>
      <td>4.37</td>
      <td>2.71</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.29</td>
      <td>Premium</td>
      <td>I</td>
      <td>VS2</td>
      <td>62.4</td>
      <td>58.0</td>
      <td>334</td>
      <td>4.20</td>
      <td>4.23</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.22</td>
      <td>Premium</td>
      <td>F</td>
      <td>SI1</td>
      <td>60.4</td>
      <td>61.0</td>
      <td>342</td>
      <td>3.88</td>
      <td>3.84</td>
      <td>2.33</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.24</td>
      <td>Very Good</td>
      <td>I</td>
      <td>VVS1</td>
      <td>62.3</td>
      <td>57.0</td>
      <td>336</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.47</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.26</td>
      <td>Very Good</td>
      <td>H</td>
      <td>SI1</td>
      <td>61.9</td>
      <td>55.0</td>
      <td>337</td>
      <td>4.07</td>
      <td>4.11</td>
      <td>2.53</td>
    </tr>
  </tbody>
</table>
</div>



* sample()


```python
(
    diamonds
    >> sample(frac = 0.001, replace = False) # frac 은 비율로 sample 갯수를 지정
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9342</th>
      <td>1.00</td>
      <td>Good</td>
      <td>I</td>
      <td>VS1</td>
      <td>63.9</td>
      <td>56.0</td>
      <td>4581</td>
      <td>6.37</td>
      <td>6.18</td>
      <td>4.01</td>
    </tr>
    <tr>
      <th>23375</th>
      <td>0.33</td>
      <td>Very Good</td>
      <td>D</td>
      <td>SI2</td>
      <td>63.3</td>
      <td>53.0</td>
      <td>631</td>
      <td>4.42</td>
      <td>4.39</td>
      <td>2.79</td>
    </tr>
    <tr>
      <th>47367</th>
      <td>0.63</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>58.8</td>
      <td>59.0</td>
      <td>1846</td>
      <td>5.68</td>
      <td>5.62</td>
      <td>3.32</td>
    </tr>
    <tr>
      <th>46917</th>
      <td>0.70</td>
      <td>Ideal</td>
      <td>J</td>
      <td>SI1</td>
      <td>62.0</td>
      <td>55.0</td>
      <td>1815</td>
      <td>5.69</td>
      <td>5.73</td>
      <td>3.54</td>
    </tr>
    <tr>
      <th>21653</th>
      <td>1.53</td>
      <td>Premium</td>
      <td>G</td>
      <td>SI1</td>
      <td>61.7</td>
      <td>59.0</td>
      <td>9747</td>
      <td>7.40</td>
      <td>7.31</td>
      <td>4.54</td>
    </tr>
    <tr>
      <th>23333</th>
      <td>1.53</td>
      <td>Very Good</td>
      <td>F</td>
      <td>VS1</td>
      <td>63.2</td>
      <td>58.0</td>
      <td>11379</td>
      <td>7.33</td>
      <td>7.30</td>
      <td>4.62</td>
    </tr>
    <tr>
      <th>31910</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>G</td>
      <td>VS1</td>
      <td>62.6</td>
      <td>57.0</td>
      <td>776</td>
      <td>4.29</td>
      <td>4.27</td>
      <td>2.68</td>
    </tr>
    <tr>
      <th>2953</th>
      <td>0.70</td>
      <td>Very Good</td>
      <td>E</td>
      <td>VVS2</td>
      <td>60.7</td>
      <td>56.0</td>
      <td>3295</td>
      <td>5.77</td>
      <td>5.82</td>
      <td>3.52</td>
    </tr>
    <tr>
      <th>3115</th>
      <td>0.92</td>
      <td>Fair</td>
      <td>F</td>
      <td>SI1</td>
      <td>66.0</td>
      <td>57.0</td>
      <td>3323</td>
      <td>6.04</td>
      <td>5.99</td>
      <td>3.97</td>
    </tr>
    <tr>
      <th>21714</th>
      <td>0.33</td>
      <td>Very Good</td>
      <td>E</td>
      <td>VS2</td>
      <td>61.9</td>
      <td>58.0</td>
      <td>627</td>
      <td>4.42</td>
      <td>4.47</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>2170</th>
      <td>0.94</td>
      <td>Good</td>
      <td>I</td>
      <td>SI2</td>
      <td>63.8</td>
      <td>60.0</td>
      <td>3134</td>
      <td>6.14</td>
      <td>6.21</td>
      <td>3.94</td>
    </tr>
    <tr>
      <th>23835</th>
      <td>1.51</td>
      <td>Ideal</td>
      <td>G</td>
      <td>SI1</td>
      <td>61.6</td>
      <td>57.0</td>
      <td>11917</td>
      <td>7.34</td>
      <td>7.31</td>
      <td>4.52</td>
    </tr>
    <tr>
      <th>42038</th>
      <td>0.54</td>
      <td>Ideal</td>
      <td>H</td>
      <td>SI1</td>
      <td>61.1</td>
      <td>56.0</td>
      <td>1268</td>
      <td>5.25</td>
      <td>5.27</td>
      <td>3.21</td>
    </tr>
    <tr>
      <th>53765</th>
      <td>0.70</td>
      <td>Very Good</td>
      <td>D</td>
      <td>SI1</td>
      <td>61.8</td>
      <td>55.0</td>
      <td>2726</td>
      <td>5.73</td>
      <td>5.76</td>
      <td>3.55</td>
    </tr>
    <tr>
      <th>13447</th>
      <td>1.00</td>
      <td>Very Good</td>
      <td>G</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>56.7</td>
      <td>5522</td>
      <td>6.44</td>
      <td>6.47</td>
      <td>3.94</td>
    </tr>
    <tr>
      <th>11777</th>
      <td>1.20</td>
      <td>Very Good</td>
      <td>J</td>
      <td>SI1</td>
      <td>61.8</td>
      <td>57.7</td>
      <td>5083</td>
      <td>6.78</td>
      <td>6.91</td>
      <td>4.23</td>
    </tr>
    <tr>
      <th>52440</th>
      <td>0.71</td>
      <td>Ideal</td>
      <td>G</td>
      <td>SI1</td>
      <td>62.1</td>
      <td>54.0</td>
      <td>2513</td>
      <td>5.72</td>
      <td>5.75</td>
      <td>3.56</td>
    </tr>
    <tr>
      <th>25111</th>
      <td>1.23</td>
      <td>Ideal</td>
      <td>D</td>
      <td>VVS2</td>
      <td>62.4</td>
      <td>55.0</td>
      <td>13653</td>
      <td>6.87</td>
      <td>6.82</td>
      <td>4.27</td>
    </tr>
    <tr>
      <th>37658</th>
      <td>0.42</td>
      <td>Premium</td>
      <td>F</td>
      <td>SI1</td>
      <td>60.8</td>
      <td>58.0</td>
      <td>992</td>
      <td>4.87</td>
      <td>4.83</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>7786</th>
      <td>1.01</td>
      <td>Good</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.4</td>
      <td>64.0</td>
      <td>4285</td>
      <td>6.29</td>
      <td>6.42</td>
      <td>3.90</td>
    </tr>
    <tr>
      <th>15437</th>
      <td>1.37</td>
      <td>Premium</td>
      <td>F</td>
      <td>SI2</td>
      <td>62.8</td>
      <td>57.0</td>
      <td>6181</td>
      <td>7.12</td>
      <td>7.08</td>
      <td>4.46</td>
    </tr>
    <tr>
      <th>7851</th>
      <td>0.90</td>
      <td>Premium</td>
      <td>D</td>
      <td>SI1</td>
      <td>62.7</td>
      <td>56.0</td>
      <td>4304</td>
      <td>6.16</td>
      <td>6.12</td>
      <td>3.85</td>
    </tr>
    <tr>
      <th>1508</th>
      <td>0.71</td>
      <td>Very Good</td>
      <td>G</td>
      <td>VS1</td>
      <td>59.3</td>
      <td>55.0</td>
      <td>2994</td>
      <td>5.88</td>
      <td>5.95</td>
      <td>3.51</td>
    </tr>
    <tr>
      <th>49890</th>
      <td>0.51</td>
      <td>Ideal</td>
      <td>D</td>
      <td>VS1</td>
      <td>61.9</td>
      <td>57.0</td>
      <td>2177</td>
      <td>5.17</td>
      <td>5.14</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>32213</th>
      <td>0.31</td>
      <td>Ideal</td>
      <td>G</td>
      <td>VVS1</td>
      <td>62.1</td>
      <td>55.0</td>
      <td>789</td>
      <td>4.34</td>
      <td>4.39</td>
      <td>2.71</td>
    </tr>
    <tr>
      <th>25366</th>
      <td>0.28</td>
      <td>Very Good</td>
      <td>D</td>
      <td>VVS1</td>
      <td>60.4</td>
      <td>59.0</td>
      <td>642</td>
      <td>4.23</td>
      <td>4.25</td>
      <td>2.56</td>
    </tr>
    <tr>
      <th>32236</th>
      <td>0.31</td>
      <td>Ideal</td>
      <td>G</td>
      <td>VVS1</td>
      <td>61.0</td>
      <td>56.0</td>
      <td>789</td>
      <td>4.36</td>
      <td>4.40</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>37836</th>
      <td>0.33</td>
      <td>Premium</td>
      <td>D</td>
      <td>VS2</td>
      <td>60.7</td>
      <td>58.0</td>
      <td>1002</td>
      <td>4.50</td>
      <td>4.46</td>
      <td>2.72</td>
    </tr>
    <tr>
      <th>897</th>
      <td>1.00</td>
      <td>Fair</td>
      <td>J</td>
      <td>VS1</td>
      <td>65.5</td>
      <td>55.0</td>
      <td>2875</td>
      <td>6.30</td>
      <td>6.25</td>
      <td>4.11</td>
    </tr>
    <tr>
      <th>50271</th>
      <td>0.58</td>
      <td>Premium</td>
      <td>F</td>
      <td>VVS2</td>
      <td>62.6</td>
      <td>56.0</td>
      <td>2238</td>
      <td>5.37</td>
      <td>5.27</td>
      <td>3.33</td>
    </tr>
    <tr>
      <th>8959</th>
      <td>1.20</td>
      <td>Very Good</td>
      <td>F</td>
      <td>SI2</td>
      <td>63.2</td>
      <td>58.0</td>
      <td>4502</td>
      <td>6.78</td>
      <td>6.74</td>
      <td>4.27</td>
    </tr>
    <tr>
      <th>21403</th>
      <td>1.57</td>
      <td>Ideal</td>
      <td>J</td>
      <td>VVS2</td>
      <td>61.4</td>
      <td>57.0</td>
      <td>9516</td>
      <td>7.50</td>
      <td>7.45</td>
      <td>4.59</td>
    </tr>
    <tr>
      <th>44002</th>
      <td>0.30</td>
      <td>Good</td>
      <td>I</td>
      <td>SI1</td>
      <td>63.5</td>
      <td>57.0</td>
      <td>394</td>
      <td>4.24</td>
      <td>4.26</td>
      <td>2.70</td>
    </tr>
    <tr>
      <th>38217</th>
      <td>0.43</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.5</td>
      <td>56.0</td>
      <td>1016</td>
      <td>4.90</td>
      <td>4.85</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>2647</th>
      <td>0.83</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI1</td>
      <td>62.7</td>
      <td>57.0</td>
      <td>3231</td>
      <td>5.96</td>
      <td>6.01</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>48878</th>
      <td>1.01</td>
      <td>Fair</td>
      <td>E</td>
      <td>I1</td>
      <td>64.5</td>
      <td>54.0</td>
      <td>2036</td>
      <td>6.31</td>
      <td>6.22</td>
      <td>4.03</td>
    </tr>
    <tr>
      <th>4430</th>
      <td>0.90</td>
      <td>Very Good</td>
      <td>G</td>
      <td>SI1</td>
      <td>63.8</td>
      <td>53.0</td>
      <td>3615</td>
      <td>6.10</td>
      <td>6.16</td>
      <td>3.91</td>
    </tr>
    <tr>
      <th>40478</th>
      <td>0.53</td>
      <td>Good</td>
      <td>E</td>
      <td>SI2</td>
      <td>63.4</td>
      <td>56.0</td>
      <td>1141</td>
      <td>5.16</td>
      <td>5.18</td>
      <td>3.28</td>
    </tr>
    <tr>
      <th>19052</th>
      <td>1.02</td>
      <td>Ideal</td>
      <td>F</td>
      <td>VS1</td>
      <td>62.2</td>
      <td>57.0</td>
      <td>7836</td>
      <td>6.39</td>
      <td>6.43</td>
      <td>3.99</td>
    </tr>
    <tr>
      <th>11781</th>
      <td>1.01</td>
      <td>Very Good</td>
      <td>E</td>
      <td>SI1</td>
      <td>63.1</td>
      <td>57.0</td>
      <td>5085</td>
      <td>6.33</td>
      <td>6.44</td>
      <td>4.03</td>
    </tr>
    <tr>
      <th>44767</th>
      <td>0.53</td>
      <td>Ideal</td>
      <td>D</td>
      <td>SI1</td>
      <td>61.6</td>
      <td>56.0</td>
      <td>1621</td>
      <td>5.20</td>
      <td>5.23</td>
      <td>3.21</td>
    </tr>
    <tr>
      <th>108</th>
      <td>0.81</td>
      <td>Ideal</td>
      <td>F</td>
      <td>SI2</td>
      <td>58.8</td>
      <td>57.0</td>
      <td>2761</td>
      <td>6.14</td>
      <td>6.11</td>
      <td>3.60</td>
    </tr>
    <tr>
      <th>14505</th>
      <td>1.00</td>
      <td>Very Good</td>
      <td>G</td>
      <td>VS2</td>
      <td>61.5</td>
      <td>58.0</td>
      <td>5860</td>
      <td>6.36</td>
      <td>6.39</td>
      <td>3.92</td>
    </tr>
    <tr>
      <th>47258</th>
      <td>0.50</td>
      <td>Very Good</td>
      <td>G</td>
      <td>VVS1</td>
      <td>60.9</td>
      <td>57.0</td>
      <td>1843</td>
      <td>5.10</td>
      <td>5.15</td>
      <td>3.12</td>
    </tr>
    <tr>
      <th>12850</th>
      <td>1.34</td>
      <td>Ideal</td>
      <td>G</td>
      <td>SI2</td>
      <td>62.0</td>
      <td>55.0</td>
      <td>5358</td>
      <td>7.06</td>
      <td>7.03</td>
      <td>4.37</td>
    </tr>
    <tr>
      <th>381</th>
      <td>0.80</td>
      <td>Good</td>
      <td>G</td>
      <td>SI1</td>
      <td>62.7</td>
      <td>57.0</td>
      <td>2810</td>
      <td>5.84</td>
      <td>5.93</td>
      <td>3.69</td>
    </tr>
    <tr>
      <th>10719</th>
      <td>0.31</td>
      <td>Ideal</td>
      <td>D</td>
      <td>SI2</td>
      <td>62.5</td>
      <td>55.0</td>
      <td>593</td>
      <td>4.34</td>
      <td>4.30</td>
      <td>2.70</td>
    </tr>
    <tr>
      <th>11827</th>
      <td>1.00</td>
      <td>Fair</td>
      <td>D</td>
      <td>SI1</td>
      <td>67.3</td>
      <td>57.0</td>
      <td>5096</td>
      <td>6.15</td>
      <td>6.04</td>
      <td>4.10</td>
    </tr>
    <tr>
      <th>6854</th>
      <td>0.91</td>
      <td>Good</td>
      <td>G</td>
      <td>VS2</td>
      <td>59.9</td>
      <td>61.0</td>
      <td>4125</td>
      <td>6.20</td>
      <td>6.33</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>18848</th>
      <td>1.54</td>
      <td>Premium</td>
      <td>I</td>
      <td>SI2</td>
      <td>60.1</td>
      <td>61.0</td>
      <td>7727</td>
      <td>7.46</td>
      <td>7.41</td>
      <td>4.47</td>
    </tr>
    <tr>
      <th>17573</th>
      <td>1.08</td>
      <td>Fair</td>
      <td>G</td>
      <td>VS1</td>
      <td>64.7</td>
      <td>60.0</td>
      <td>7076</td>
      <td>6.44</td>
      <td>6.41</td>
      <td>4.16</td>
    </tr>
    <tr>
      <th>916</th>
      <td>0.84</td>
      <td>Ideal</td>
      <td>G</td>
      <td>SI2</td>
      <td>61.0</td>
      <td>56.0</td>
      <td>2879</td>
      <td>6.13</td>
      <td>6.10</td>
      <td>3.73</td>
    </tr>
    <tr>
      <th>47046</th>
      <td>0.50</td>
      <td>Ideal</td>
      <td>D</td>
      <td>VS2</td>
      <td>62.9</td>
      <td>54.0</td>
      <td>1819</td>
      <td>5.09</td>
      <td>5.05</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>18685</th>
      <td>1.53</td>
      <td>Good</td>
      <td>E</td>
      <td>SI2</td>
      <td>57.1</td>
      <td>56.0</td>
      <td>7643</td>
      <td>7.69</td>
      <td>7.65</td>
      <td>4.38</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
    >> sample(n = 3, replace = True) # frac 은 비율로 sample 갯수를 지정
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18978</th>
      <td>1.51</td>
      <td>Very Good</td>
      <td>J</td>
      <td>SI1</td>
      <td>60.9</td>
      <td>59.0</td>
      <td>7812</td>
      <td>7.33</td>
      <td>7.41</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>8912</th>
      <td>1.00</td>
      <td>Premium</td>
      <td>G</td>
      <td>SI1</td>
      <td>62.5</td>
      <td>59.0</td>
      <td>4493</td>
      <td>6.35</td>
      <td>6.29</td>
      <td>3.95</td>
    </tr>
    <tr>
      <th>25975</th>
      <td>2.19</td>
      <td>Premium</td>
      <td>I</td>
      <td>SI2</td>
      <td>62.5</td>
      <td>58.0</td>
      <td>15169</td>
      <td>8.31</td>
      <td>8.26</td>
      <td>5.18</td>
    </tr>
  </tbody>
</table>
</div>



* distinct()


```python
(
    diamonds 
    >> distinct(X.cut)
#     >> distinct(X.clarity)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.24</td>
      <td>Very Good</td>
      <td>J</td>
      <td>VVS2</td>
      <td>62.8</td>
      <td>57.0</td>
      <td>336</td>
      <td>3.94</td>
      <td>3.96</td>
      <td>2.48</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.22</td>
      <td>Fair</td>
      <td>E</td>
      <td>VS2</td>
      <td>65.1</td>
      <td>61.0</td>
      <td>337</td>
      <td>3.87</td>
      <td>3.78</td>
      <td>2.49</td>
    </tr>
  </tbody>
</table>
</div>



* mask()


```python
(
    diamonds 
    >> select(X)
    >> mask(X.cut == 'Ideal')
    >> head(3)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>J</td>
      <td>VS1</td>
      <td>62.8</td>
      <td>56.0</td>
      <td>340</td>
      <td>3.93</td>
      <td>3.90</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.31</td>
      <td>Ideal</td>
      <td>J</td>
      <td>SI2</td>
      <td>62.2</td>
      <td>54.0</td>
      <td>344</td>
      <td>4.35</td>
      <td>4.37</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>



* mask() 복합 조건 사용도 가능


```python
(
    diamonds 
    >> mask(X.cut == 'Ideal', X.color == 'E', X.table <55, X.price <500)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>26683</th>
      <td>0.33</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.2</td>
      <td>54.0</td>
      <td>427</td>
      <td>4.44</td>
      <td>4.46</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>32297</th>
      <td>0.34</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.4</td>
      <td>54.0</td>
      <td>454</td>
      <td>4.49</td>
      <td>4.52</td>
      <td>2.81</td>
    </tr>
    <tr>
      <th>40928</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.6</td>
      <td>54.0</td>
      <td>499</td>
      <td>4.32</td>
      <td>4.35</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>50623</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.1</td>
      <td>54.0</td>
      <td>401</td>
      <td>4.32</td>
      <td>4.35</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>50625</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.0</td>
      <td>54.0</td>
      <td>401</td>
      <td>4.33</td>
      <td>4.35</td>
      <td>2.69</td>
    </tr>
  </tbody>
</table>
</div>



* mask()는 filter_by() 로 사용되기도 함


```python
(
    diamonds
    >> filter_by(X.cut == 'Ideal', X.color == 'E', X.table <55, X.price <500)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>26683</th>
      <td>0.33</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.2</td>
      <td>54.0</td>
      <td>427</td>
      <td>4.44</td>
      <td>4.46</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>32297</th>
      <td>0.34</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.4</td>
      <td>54.0</td>
      <td>454</td>
      <td>4.49</td>
      <td>4.52</td>
      <td>2.81</td>
    </tr>
    <tr>
      <th>40928</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.6</td>
      <td>54.0</td>
      <td>499</td>
      <td>4.32</td>
      <td>4.35</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>50623</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.1</td>
      <td>54.0</td>
      <td>401</td>
      <td>4.32</td>
      <td>4.35</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>50625</th>
      <td>0.30</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>62.0</td>
      <td>54.0</td>
      <td>401</td>
      <td>4.33</td>
      <td>4.35</td>
      <td>2.69</td>
    </tr>
  </tbody>
</table>
</div>



* pull() : 결과로 산출되는 것의 데이터 타입이 DataFrame이 아닌 것에 주의하자


```python
(
    diamonds 
    >> filter_by(X.cut == 'Ideal', X.color == 'E', X.table <55, X.price <500) 
    >> pull('carat')
)
```




    26683    0.33
    32297    0.34
    40928    0.30
    50623    0.30
    50625    0.30
    Name: carat, dtype: float64



## DataFrame transformation

## mutate()


```python
(
    diamonds 
    >> mutate(x_plus_y = X.x + X.y)
    >> select(columns_from('x'))
    >> head(3)
)
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
      <th>x</th>
      <th>y</th>
      <th>z</th>
      <th>x_plus_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
      <td>7.93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
      <td>7.73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
      <td>8.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds 
    >> mutate(x_plus_y = X.x + X.y, y_div_z = (X.y / X.z)) # multiple condition available
    >> select(columns_from('x'))
    >> head(3)
)
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
      <th>x</th>
      <th>y</th>
      <th>z</th>
      <th>x_plus_y</th>
      <th>y_div_z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
      <td>7.93</td>
      <td>1.637860</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
      <td>7.73</td>
      <td>1.662338</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
      <td>8.12</td>
      <td>1.761905</td>
    </tr>
  </tbody>
</table>
</div>



* transmute() : mutate and select the created values


```python
(
    diamonds 
    >> transmute(x_plus_y = X.x + X.y, y_div_z = (X.y / X.z)) # multiple condition available
#     >> select(columns_from('x'))
    >> head(3)
)
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
      <th>y_div_z</th>
      <th>x_plus_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.637860</td>
      <td>7.93</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.662338</td>
      <td>7.73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.761905</td>
      <td>8.12</td>
    </tr>
  </tbody>
</table>
</div>



## Grouping()

* group_by() and ungroup()


```python
(
    diamonds
    >> group_by(X.cut)
    >> mutate(price_lead = lead(X.price), price_lag = lag(X.price))
    >> head(2)
    >> select(X.cut, X.price, X.price_lag, X.price_lead)
)
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
      <th>cut</th>
      <th>price</th>
      <th>price_lag</th>
      <th>price_lead</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>Fair</td>
      <td>337</td>
      <td>NaN</td>
      <td>2757.0</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Fair</td>
      <td>2757</td>
      <td>337.0</td>
      <td>2759.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Good</td>
      <td>327</td>
      <td>NaN</td>
      <td>335.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Good</td>
      <td>335</td>
      <td>327.0</td>
      <td>339.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Ideal</td>
      <td>326</td>
      <td>NaN</td>
      <td>340.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Ideal</td>
      <td>340</td>
      <td>326.0</td>
      <td>344.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Premium</td>
      <td>326</td>
      <td>NaN</td>
      <td>334.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>334</td>
      <td>326.0</td>
      <td>342.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Very Good</td>
      <td>336</td>
      <td>NaN</td>
      <td>336.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Very Good</td>
      <td>336</td>
      <td>336.0</td>
      <td>337.0</td>
    </tr>
  </tbody>
</table>
</div>



### Reshaping

* arrange()


```python
(
    diamonds
    >> arrange(X.table, ascending = False)
    >> head(5)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24932</th>
      <td>2.01</td>
      <td>Fair</td>
      <td>F</td>
      <td>SI1</td>
      <td>58.6</td>
      <td>95.0</td>
      <td>13387</td>
      <td>8.32</td>
      <td>8.31</td>
      <td>4.87</td>
    </tr>
    <tr>
      <th>50773</th>
      <td>0.81</td>
      <td>Fair</td>
      <td>F</td>
      <td>SI2</td>
      <td>68.8</td>
      <td>79.0</td>
      <td>2301</td>
      <td>5.26</td>
      <td>5.20</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>51342</th>
      <td>0.79</td>
      <td>Fair</td>
      <td>G</td>
      <td>SI1</td>
      <td>65.3</td>
      <td>76.0</td>
      <td>2362</td>
      <td>5.52</td>
      <td>5.13</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>52860</th>
      <td>0.50</td>
      <td>Fair</td>
      <td>E</td>
      <td>VS2</td>
      <td>79.0</td>
      <td>73.0</td>
      <td>2579</td>
      <td>5.21</td>
      <td>5.18</td>
      <td>4.09</td>
    </tr>
    <tr>
      <th>49375</th>
      <td>0.70</td>
      <td>Fair</td>
      <td>H</td>
      <td>VS1</td>
      <td>62.0</td>
      <td>73.0</td>
      <td>2100</td>
      <td>5.65</td>
      <td>5.54</td>
      <td>3.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
    >> group_by(X.cut) 
    >> arrange(X.price)
    >> head(3) 
    >> ungroup()
    >> mask(X.carat < 0.23)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>0.22</td>
      <td>Fair</td>
      <td>E</td>
      <td>VS2</td>
      <td>65.1</td>
      <td>61.0</td>
      <td>337</td>
      <td>3.87</td>
      <td>3.78</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.22</td>
      <td>Premium</td>
      <td>F</td>
      <td>SI1</td>
      <td>60.4</td>
      <td>61.0</td>
      <td>342</td>
      <td>3.88</td>
      <td>3.84</td>
      <td>2.33</td>
    </tr>
  </tbody>
</table>
</div>



* rename()


```python
(
    diamonds
    >> rename(CUT = X.cut, COLOR = 'color') # variable ways to rename columns
    >> head(2)
)
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
      <th>carat</th>
      <th>CUT</th>
      <th>COLOR</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>



* gather()


```python
(
    diamonds
    >> gather('variable', 'value',['price', 'depth', 'x','y','z']) # 기존 컬럼들을 유지한 상태에서 진행된다는 점에 주의할 것
    >> group_by('variable')
    >> head(3)
)
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>table</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>53940</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.0</td>
      <td>depth</td>
      <td>61.50</td>
    </tr>
    <tr>
      <th>53941</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>depth</td>
      <td>59.80</td>
    </tr>
    <tr>
      <th>53942</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>65.0</td>
      <td>depth</td>
      <td>56.90</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.0</td>
      <td>price</td>
      <td>326.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>price</td>
      <td>326.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>65.0</td>
      <td>price</td>
      <td>327.00</td>
    </tr>
    <tr>
      <th>107880</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.0</td>
      <td>x</td>
      <td>3.95</td>
    </tr>
    <tr>
      <th>107881</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>x</td>
      <td>3.89</td>
    </tr>
    <tr>
      <th>107882</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>65.0</td>
      <td>x</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>161820</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.0</td>
      <td>y</td>
      <td>3.98</td>
    </tr>
    <tr>
      <th>161821</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>y</td>
      <td>3.84</td>
    </tr>
    <tr>
      <th>161822</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>65.0</td>
      <td>y</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>215760</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>55.0</td>
      <td>z</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>215761</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>61.0</td>
      <td>z</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>215762</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>65.0</td>
      <td>z</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    diamonds
    >> gather('key', 'value')
    >> head(5)
)
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
      <th>key</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>carat</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>carat</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>carat</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>carat</td>
      <td>0.29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>carat</td>
      <td>0.31</td>
    </tr>
  </tbody>
</table>
</div>



* add_id = True : gather 했던 컬럼을 다시 원상태로 되돌리기 위해서 필요함


```python
(
    diamonds
    >> select(X.depth, X.x, X.y)
    >> head(100)
    >> gather('key', 'value', ['x','y'], add_id=True) # 시간이 오래 걸림. 멈추어야 할 지경. 주의할 것
    >> head(5)
)
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
      <th>depth</th>
      <th>_ID</th>
      <th>key</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>61.5</td>
      <td>0</td>
      <td>x</td>
      <td>3.95</td>
    </tr>
    <tr>
      <th>1</th>
      <td>59.8</td>
      <td>1</td>
      <td>x</td>
      <td>3.89</td>
    </tr>
    <tr>
      <th>2</th>
      <td>56.9</td>
      <td>2</td>
      <td>x</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>62.4</td>
      <td>3</td>
      <td>x</td>
      <td>4.20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>63.3</td>
      <td>4</td>
      <td>x</td>
      <td>4.34</td>
    </tr>
  </tbody>
</table>
</div>



* spread()


```python
(
    d 
    >> select(X.x, X.y) 
    >> head(100)
    >> gather('key', 'value', add_id = True)
#     >> gather('key', 'value')
    # now spread again
    >> spread(X.key, X.value)
    >> head(5)
 )
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
      <th>_ID</th>
      <th>x</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3.95</td>
      <td>3.98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>3.89</td>
      <td>3.84</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>4.05</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>4.20</td>
      <td>4.23</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>4.34</td>
      <td>4.35</td>
    </tr>
  </tbody>
</table>
</div>



* spread()로 되돌릴 때에는 type이 무조건 object로 변경되는데, type을 유지하기 위해서 필요한 옵션이 convert = True


```python
d = diamonds
```


```python
elongated = diamonds >> gather('variable', 'value', add_id=True)
```


```python
widened = elongated >> spread(X.variable, X.value)
```

    * 하지만 형 변환이 이루어지지 않은 경우에는 아래처럼 형이 동일하다.


```python
widened.dtypes
```




    _ID         int64
    carat      object
    clarity    object
    color      object
    cut        object
    depth      object
    price      object
    table      object
    x          object
    y          object
    z          object
    dtype: object




```python
widened = elongated >> spread(X.variable, X.value, convert=True)
```


```python
widened.dtypes
```




    _ID          int64
    carat      float64
    clarity     object
    color       object
    cut         object
    depth      float64
    price        int64
    table      float64
    x          float64
    y          float64
    z          float64
    dtype: object



* separate()
* 컬럼을 여러 컬럼으로 나누는 것
        * separate(column, into, sep="[\W]+", remove=True, convert=False, extra='drop', fill='right')
* 다음과 같은 argument가 가능함
        * column: the column to split.
        * into: the names of the new columns.
        * sep: either a regex string or integer positions to split the column on.
        * remove: boolean indicating whether to remove the original column.
        * convert: boolean indicating whether the new columns should be converted to the appropriate type (same as in spread above).
        * extra: either drop, where split pieces beyond the specified new columns are dropped, or merge, where the final split piece contains the remainder of the original column.
        * fill: either right, where np.nan values are filled in the right-most columns for missing pieces, or left where np.nan values are filled in the left-most columns.


```python
d = pd.read_csv('dfply_example.txt')
```


```python
d
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
      <th>a</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-a-3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1-b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1-c-3-4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9-d-1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



* 두개의 컬럼을 만들고, 기존 것은 없애고, type은 맞게 넣어주고, 나머지 컬럼들을 drop하고 값들은 나머지 값들은 오른쪽부터 채워주자


```python
(
    d
    >> separate(X.a, ['col1', 'col2'], remove = True, convert=True, extra='drop', fill='right')
)
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
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>c</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>d</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



* 두개의 컬럼을 만들고, 기존 것은 남겨두며, 나머지 컬럼들을 merge 해서 가장 오른쪽 컬럼에 채워준다.


```python
(
    d
    >> separate(X.a, ['col1', 'col2'], remove = False, convert=True, extra='merge', fill='right')
)
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
      <th>a</th>
      <th>col1</th>
      <th>col2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-a-3</td>
      <td>1</td>
      <td>a-3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1-b</td>
      <td>1</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1-c-3-4</td>
      <td>1</td>
      <td>c-3-4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9-d-1</td>
      <td>9</td>
      <td>d-1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



* 3개의 컬럼으로 나눠주고, 기존 것은 지워준다. 나눌 때의 기준은 2번째, 4번째를 기준으로 함. 남은 것들을 모아서 오른쪽 컬럼에 채워주자


```python
(
    d
    >> separate(X.a, ['col1', 'col2','col3'], sep = [2,4], remove = True, convert=True, extra='merge', fill='right')
)
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
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1-</td>
      <td>a-</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1-</td>
      <td>b</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1-</td>
      <td>c-</td>
      <td>3-4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9-</td>
      <td>d-</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



* unite()
* separate()의 반대로 column을 합치는 것
* 합쳐지는 column의 type은 string으로 바뀐다.
        * unite(colname, *args, sep='_', remove = True, na_action = 'maintain')
* 아래와 같은 argument가 가능함
        * colname: the name of the new joined column.
        **args: list of columns to be joined, which can be strings, symbolic, or integer positions.
        * sep: the string separator to join the columns with.
        * remove: boolean indicating whether or not to remove the original columns.
        * na_action: can be one of "maintain" (the default), "ignore", or "as_string". 
            * The default "maintain" will make the new column row a NaN value if any of the original column cells at that row contained NaN. 
            * "ignore" will treat any NaN value as an empty string during joining. 
            * "as_string" will convert any NaN value to the string "nan" prior to joining.

* example data를 우선 가져와보자


```python
d = pd.read_csv('dfply_example_unite.txt', keep_default_na=True)
```


```python
d
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
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>c</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>



* X.a 컬럼과 'b' 이름을 가진 컬럼, 그리고 index로 2인 (세번째) 컬럼을 합쳐서 이름을 'united'라고 하자, 기존 컬럼은 그대로 두고, NaN 값들은 유지한 상태로 만들어줘라


```python
(
    d 
    >> unite('united', X.a, 'b',2, remove=False, na_action='maintain')
)
```

    ['a', 'b', 'c'] _ False maintain





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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>united</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>True</td>
      <td>1_ a_ True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>False</td>
      <td>2_ b_ False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>c</td>
      <td></td>
      <td>3_ c_</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    d
    >> unite('united', ['a','b','c'], remove=True, na_action='ignore', sep="*")
)
```

    ['a', 'b', 'c'] * True ignore





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
      <th>united</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1* a* True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2* b* False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3* c*</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    d
    >> unite('united', d.columns, remove=True, na_action='as_string', sep="*")
)
```

    ['a', 'b', 'c'] * True as_string





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
      <th>united</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1* a* True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2* b* False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3* c*</td>
    </tr>
  </tbody>
</table>
</div>



### Joining

* 아래와 같은 join 함수들이 가능함
        * inner_join(other, by='column')
        * outer_join(other, by='column')
        * right_join(other, by='column')
        * left_join(other, by='column')
        * semi_join(other, by='column')
        * anti_join(other, by='column')

* 기본적인 사용법은 아래와 같음


```python
a = pd.DataFrame({
    'x1':['A', 'B', 'C'],
    'x2':[1,2,3]
})

b = pd.DataFrame({
    'x1':['A','B','D'],
    'x3':[True, False, True]
})
```


```python
a
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
b
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
      <th>x1</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



* inner_join()


```python
(
    a
    >> inner_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



* outer_join() or full_join()


```python
(
    a
    >> outer_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



* left_join()


```python
(
    a
    >> left_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



* right_join()


```python
(
    a
    >> right_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



* semi_join()


```python
(
    a
    >> semi_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



* anti_join()


```python
(
    a
    >> anti_join(b, by='x1')
)
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



### set operation

* row를 기준으로 하는 합치기
* 아래와 같은 함수가 있음
        * union()
        * intersect()
        * set_diff()
* 공통적으로 아래와 같은 인자를 사용
        * other: the DataFrame to compare to
        * index: a boolean (default False) indicating whether to consider the pandas index during comparison.
        * keep: string (default "first") to be passed through to .drop_duplicates() controlling how to handle duplicate rows.
    


```python
a = pd.DataFrame({
        'x1':['A','B','C'],
        'x2':[1,2,3]
    })
c = pd.DataFrame({
      'x1':['B','C','D'],
      'x2':[2,3,4]
})
```


```python
a
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
c
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



* union()


```python
(
    a
    >> union(c)
)
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



* intersect()


```python
(
    a
    >> intersect(c)
)
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



* set_diff()


```python
(
    a
    >> set_diff(c)
)
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### binding

* bind_rows()
* 행 합치기


```python
a
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
      <th>x1</th>
      <th>x2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
b
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
      <th>x1</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    a
    >> bind_rows(b, join='inner')
)
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
      <th>x1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
    </tr>
    <tr>
      <th>0</th>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    a
    >> bind_rows(b, join='outer')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>NaN</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>D</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



* bind_cols()
* 열합치기


```python
(
    a
    >> bind_cols(b, join='outer')
)
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
      <th>x1</th>
      <th>x2</th>
      <th>x1</th>
      <th>x3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>1</td>
      <td>A</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>2</td>
      <td>B</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
      <td>D</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### summarize()


```python
(
    diamonds
    >> summarise(price_mean=X.price.mean(), price_std = X.price.std())
#     >> head(3)
)
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
      <th>price_mean</th>
      <th>price_std</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3932.799722</td>
      <td>3989.439738</td>
    </tr>
  </tbody>
</table>
</div>



* summarise with group_by()


```python
(
    diamonds
    >> group_by('cut')
    >> summarise(price_mean = X.price.mean(), price_std = X.price.std())
)
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
      <th>cut</th>
      <th>price_mean</th>
      <th>price_std</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>4358.757764</td>
      <td>3560.386612</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3928.864452</td>
      <td>3681.589584</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>3457.541970</td>
      <td>3808.401172</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>4584.257704</td>
      <td>4349.204961</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>3981.759891</td>
      <td>3935.862161</td>
    </tr>
  </tbody>
</table>
</div>



* summarise_each()
* 일반적인 형태의 summarize() 함수 적용 형태
* group_by()와 함께 사용 가능


```python
(
    diamonds 
    >> group_by(X.cut)
    >> summarise_each([np.mean, np.var], X.price, X.depth) # mean, var 을 price, depth 변수에 적용하여 4개의 컬럼이 만들어 지는 예. 함수갯수 * 변수갯수 만큼의 컬럼이 생기는 것
)
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
      <th>cut</th>
      <th>price_mean</th>
      <th>price_var</th>
      <th>depth_mean</th>
      <th>depth_var</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>4358.757764</td>
      <td>1.266848e+07</td>
      <td>64.041677</td>
      <td>13.266319</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3928.864452</td>
      <td>1.355134e+07</td>
      <td>62.365879</td>
      <td>4.705224</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>3457.541970</td>
      <td>1.450325e+07</td>
      <td>61.709401</td>
      <td>0.516274</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>4584.257704</td>
      <td>1.891421e+07</td>
      <td>61.264673</td>
      <td>1.342755</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>3981.759891</td>
      <td>1.548973e+07</td>
      <td>61.818275</td>
      <td>1.900466</td>
    </tr>
  </tbody>
</table>
</div>



### embeded column functions

* window functions : input, output 벡터 크기가 동일
* summary functions : output 벡터의 크기가 축약

* lead() and lag()
        * lead() : add NaN values upward
        * lag() : add NaN values downward


```python
(
    diamonds
    >> mutate(price_lead= lead(X.price,3), price_lag = lag(X.price,2))
    >> select(X.price, -2, -1)
    >> head(6)
)
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
      <th>price</th>
      <th>price_lag</th>
      <th>price_lead</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>NaN</td>
      <td>334.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>NaN</td>
      <td>335.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>326.0</td>
      <td>336.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>326.0</td>
      <td>336.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>327.0</td>
      <td>337.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>336</td>
      <td>334.0</td>
      <td>337.0</td>
    </tr>
  </tbody>
</table>
</div>



* between()
* 해당 컬럼의 값이 주어진 값 사이에 있는지를 T/F 반환


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_btwn = between(X.price, 330,340))
    >> head(10)
)
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
      <th>price</th>
      <th>price_btwn</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>336</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>336</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>337</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>337</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>338</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### rank() : 순위를 매겨주기
        * dense_rank() : 동일한 값 이후를 바로 다음 순위로 처리
        * min_rank() : 동일한 값 이후를 동일값의 갯수만큼 띄어서 처리
        * row_number() : 동일한 값에 대해서 임의로 순서 인덱스를 부여함


* dense_rank()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_drank = dense_rank(X.price, ascending=True)) # 큰것부터 등수를 매기려면 ascending = False 로 처리함.
    >> head(5)
)
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
      <th>price</th>
      <th>price_drank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



* min_rank()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_drank = min_rank(X.price, ascending=True)) # 큰것부터 등수를 매기려면 ascending = False 로 처리함.
    >> head(5)
)
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
      <th>price</th>
      <th>price_drank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



* row_number()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_drank = row_number(X.price, ascending=True)) # 큰것부터 등수를 매기려면 ascending = False 로 처리함.
    >> head(5)
)
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
      <th>price</th>
      <th>price_drank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



* 순위에 대한 비율 계산
        * percent_rank()

* percent_rank


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cume_dist = percent_rank(X.price)) # ascending=False 옵션을 주면 반대로 계산 가능
    >> head(5)
)
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
      <th>price</th>
      <th>price_cume_dist</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>0.000037</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>0.000056</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>0.000074</td>
    </tr>
  </tbody>
</table>
</div>



* cumsum : 누적합


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cumsum = cumsum(X.price))
    >> head(5)
)
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
      <th>price</th>
      <th>price_cumsum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>326</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>979</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>1313</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>1648</td>
    </tr>
  </tbody>
</table>
</div>



* cummean()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cummean = cummean(X.price))
    >> head(5)
)
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
      <th>price</th>
      <th>price_cummean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>326.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>326.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>326.333333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>328.250000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>329.600000</td>
    </tr>
  </tbody>
</table>
</div>



* cummax()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cummax = cummax(X.price))
    >> head(5)
)
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
      <th>price</th>
      <th>price_cummax</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>327.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>334.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>335.0</td>
    </tr>
  </tbody>
</table>
</div>



* cummin()


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cummin = cummin(X.price))
    >> head(5)
)
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
      <th>price</th>
      <th>price_cummin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>326.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>326.0</td>
    </tr>
  </tbody>
</table>
</div>



* cumprod


```python
(
    diamonds
    >> select(X.price)
    >> mutate(price_cumprod = cumprod(X.price))
    >> head(5)
)
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
      <th>price</th>
      <th>price_cumprod</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>326</td>
      <td>326</td>
    </tr>
    <tr>
      <th>1</th>
      <td>326</td>
      <td>106276</td>
    </tr>
    <tr>
      <th>2</th>
      <td>327</td>
      <td>34752252</td>
    </tr>
    <tr>
      <th>3</th>
      <td>334</td>
      <td>11607252168</td>
    </tr>
    <tr>
      <th>4</th>
      <td>335</td>
      <td>3888429476280</td>
    </tr>
  </tbody>
</table>
</div>



### summary functions

* mean()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_mean = mean(X.price))
)
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
      <th>cut</th>
      <th>price_mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>4358.757764</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3928.864452</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>3457.541970</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>4584.257704</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>3981.759891</td>
    </tr>
  </tbody>
</table>
</div>



* first()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_first=first(X.price))
)
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
      <th>cut</th>
      <th>price_first</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>337</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>327</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>326</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>326</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>336</td>
    </tr>
  </tbody>
</table>
</div>



* last()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_last=last(X.price))
)
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
      <th>cut</th>
      <th>price_last</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>2747</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>2757</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>2757</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>2757</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>2757</td>
    </tr>
  </tbody>
</table>
</div>



* nth()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_penultimate = nth(X.price, -3))
)
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
      <th>cut</th>
      <th>price_penultimate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>2743</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>2753</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>2756</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>2756</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>2757</td>
    </tr>
  </tbody>
</table>
</div>



* n()
    * distinct가 아닌 그야말로 행의 갯수를 세는 것


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_n = n(X.price), color_n= n(X.color))
)
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
      <th>cut</th>
      <th>color_n</th>
      <th>price_n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>1610</td>
      <td>1610</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>4906</td>
      <td>4906</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>21551</td>
      <td>21551</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>13791</td>
      <td>13791</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>12082</td>
      <td>12082</td>
    </tr>
  </tbody>
</table>
</div>



* n_distinct()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_ndistinct = n_distinct(X.price), price_n= n(X.price))
)
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
      <th>cut</th>
      <th>price_n</th>
      <th>price_ndistinct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>1610</td>
      <td>1267</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>4906</td>
      <td>3086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>21551</td>
      <td>7281</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>13791</td>
      <td>6014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>12082</td>
      <td>5840</td>
    </tr>
  </tbody>
</table>
</div>



* IQR()
    * ineter quantile range


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_iqr = IQR(X.price))
)
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
      <th>cut</th>
      <th>price_iqr</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>3155.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3883.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>3800.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>5250.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>4460.75</td>
    </tr>
  </tbody>
</table>
</div>



* colmin()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_min= colmin(X.price))

)
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
      <th>cut</th>
      <th>price_min</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>337</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>327</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>326</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>326</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>336</td>
    </tr>
  </tbody>
</table>
</div>



* colmax()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_max = colmax(X.price))
)
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
      <th>cut</th>
      <th>price_max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>18574</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>18788</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>18806</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>18823</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>18818</td>
    </tr>
  </tbody>
</table>
</div>



* median()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_median = median(X.price))
)
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
      <th>cut</th>
      <th>price_median</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>3282.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3050.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>1810.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>3185.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>2648.0</td>
    </tr>
  </tbody>
</table>
</div>



* var()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_var = var(X.price))
)
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
      <th>cut</th>
      <th>price_var</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>1.267635e+07</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>1.355410e+07</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>1.450392e+07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>1.891558e+07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>1.549101e+07</td>
    </tr>
  </tbody>
</table>
</div>



* sd()


```python
(
    diamonds
    >> group_by(X.cut)
    >> summarise(price_sd = sd(X.price))
)
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
      <th>cut</th>
      <th>price_sd</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>3560.386612</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>3681.589584</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>3808.401172</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>4349.204961</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>3935.862161</td>
    </tr>
  </tbody>
</table>
</div>



### Extending dfply with custom functions

* function을 직접 만들어 사용할 수 있음

### Case 1: A custom 'pipe' function with @dfpipe

* 보통은 아래와 같이 함수를 정의하여 사용함


```python
def crosstab(df, index, columns):
    return pd.crosstab(index, columns)
```


```python
pd.crosstab(diamonds.cut, diamonds.color)
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
      <th>color</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
      <th>G</th>
      <th>H</th>
      <th>I</th>
      <th>J</th>
    </tr>
    <tr>
      <th>cut</th>
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
      <th>Fair</th>
      <td>163</td>
      <td>224</td>
      <td>312</td>
      <td>314</td>
      <td>303</td>
      <td>175</td>
      <td>119</td>
    </tr>
    <tr>
      <th>Good</th>
      <td>662</td>
      <td>933</td>
      <td>909</td>
      <td>871</td>
      <td>702</td>
      <td>522</td>
      <td>307</td>
    </tr>
    <tr>
      <th>Ideal</th>
      <td>2834</td>
      <td>3903</td>
      <td>3826</td>
      <td>4884</td>
      <td>3115</td>
      <td>2093</td>
      <td>896</td>
    </tr>
    <tr>
      <th>Premium</th>
      <td>1603</td>
      <td>2337</td>
      <td>2331</td>
      <td>2924</td>
      <td>2360</td>
      <td>1428</td>
      <td>808</td>
    </tr>
    <tr>
      <th>Very Good</th>
      <td>1513</td>
      <td>2400</td>
      <td>2164</td>
      <td>2299</td>
      <td>1824</td>
      <td>1204</td>
      <td>678</td>
    </tr>
  </tbody>
</table>
</div>



* 이 함수를 pipe operation에서 사용하려면 아래와 같이 함

* 우선 crosstab 함수를 pipe에서 사용하려고 할 때 에러가 발생하는 것을 보자


```python
(
    diamonds
    >> crosstab(X.cut, X.color)
)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-347-9d04b4ac9ff3> in <module>()
          1 (
          2     diamonds
    ----> 3     >> crosstab(X.cut, X.color)
          4 )


    TypeError: crosstab() missing 1 required positional argument: 'columns'


* 이제 이 함수를 pipe에서 사용가능하도록 바꿔보자


```python
@dfpipe
def crosstab(df, index, columns):
    return pd.crosstab(index, columns)
```

* 이제 pipe 연산자를 사용해보자


```python
(
    diamonds
    >> crosstab(X.cut, X.color)
)
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
      <th>color</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
      <th>G</th>
      <th>H</th>
      <th>I</th>
      <th>J</th>
    </tr>
    <tr>
      <th>cut</th>
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
      <th>Fair</th>
      <td>163</td>
      <td>224</td>
      <td>312</td>
      <td>314</td>
      <td>303</td>
      <td>175</td>
      <td>119</td>
    </tr>
    <tr>
      <th>Good</th>
      <td>662</td>
      <td>933</td>
      <td>909</td>
      <td>871</td>
      <td>702</td>
      <td>522</td>
      <td>307</td>
    </tr>
    <tr>
      <th>Ideal</th>
      <td>2834</td>
      <td>3903</td>
      <td>3826</td>
      <td>4884</td>
      <td>3115</td>
      <td>2093</td>
      <td>896</td>
    </tr>
    <tr>
      <th>Premium</th>
      <td>1603</td>
      <td>2337</td>
      <td>2331</td>
      <td>2924</td>
      <td>2360</td>
      <td>1428</td>
      <td>808</td>
    </tr>
    <tr>
      <th>Very Good</th>
      <td>1513</td>
      <td>2400</td>
      <td>2164</td>
      <td>2299</td>
      <td>1824</td>
      <td>1204</td>
      <td>678</td>
    </tr>
  </tbody>
</table>
</div>



### case 2: A function that works with symbolic objects using @make_symbolic

* 예를 들어, 아래의 데이터에서 string 타입의 날짜를 date 타입으로 바꾸는 작업을 생각해보자


```python
sales = pd.DataFrame(dict(date=['7/10/17','7/11/17','7/12/17','7/13/17','7/14/17'],
                          sales=[1220, 1592, 908, 1102, 1395]))
```


```python
sales
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
      <th>date</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/10/17</td>
      <td>1220</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/11/17</td>
      <td>1592</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/12/17</td>
      <td>908</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/13/17</td>
      <td>1102</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/14/17</td>
      <td>1395</td>
    </tr>
  </tbody>
</table>
</div>



* 만약 pd.to_datetime 함수를 pipe 연산에서 사용한다고 해보자 ==> 에러가 발생한다.


```python
(
    sales
    >> mutate(pd_date=pd.to_datetime(X.date, infer_datetime_format=True))
)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-353-55b959c71837> in <module>()
          1 (
          2     sales
    ----> 3     >> mutate(pd_date=pd.to_datetime(X.date, infer_datetime_format=True))
          4 )


    ~/venv04/lib/python3.5/site-packages/pandas/core/tools/datetimes.py in to_datetime(arg, errors, dayfirst, yearfirst, utc, box, format, exact, unit, infer_datetime_format, origin)
        369     if isinstance(arg, tslib.Timestamp):
        370         result = arg
    --> 371     elif isinstance(arg, ABCSeries):
        372         from pandas import Series
        373         values = _convert_listlike(arg._values, True, format)


    ~/venv04/lib/python3.5/site-packages/pandas/core/dtypes/generic.py in _check(cls, inst)
          7     @classmethod
          8     def _check(cls, inst):
    ----> 9         return getattr(inst, attr, '_typ') in comp
         10 
         11     dct = dict(__instancecheck__=_check, __subclasscheck__=_check)


    TypeError: __index__ returned non-int (type Intention)


* 이 함수는 그냥 판다스 함수의 일반적 용법에 따라 사용해야 하는 것이다.


```python
pd.to_datetime(sales.date)
```




    0   2017-07-10
    1   2017-07-11
    2   2017-07-12
    3   2017-07-13
    4   2017-07-14
    Name: date, dtype: datetime64[ns]



* 이 좋은 함수를 pipe 연산에서 사용하고 싶은 것이 핵심!
* decorator를 사용해서 아래와 같이 한다.


```python
@make_symbolic
def to_datetime(series, infer_datetime_format=True):
    return pd.to_datetime(series, infer_datetime_format = infer_datetime_format)
```

* 이제 pipe 연산을 통해서 확인해보자


```python
(
    sales
    >> mutate(pd_date= to_datetime(X.date))
)
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
      <th>date</th>
      <th>sales</th>
      <th>pd_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7/10/17</td>
      <td>1220</td>
      <td>2017-07-10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7/11/17</td>
      <td>1592</td>
      <td>2017-07-11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7/12/17</td>
      <td>908</td>
      <td>2017-07-12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7/13/17</td>
      <td>1102</td>
      <td>2017-07-13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7/14/17</td>
      <td>1395</td>
      <td>2017-07-14</td>
    </tr>
  </tbody>
</table>
</div>



* decorator로 정의가 된 함수는 아래와 같은 용도로 사용할 수도 있다.


```python
to_datetime(sales.date)
```




    0   2017-07-10
    1   2017-07-11
    2   2017-07-12
    3   2017-07-13
    4   2017-07-14
    Name: date, dtype: datetime64[ns]



### Advanced: understanding base dfply decorators


```python
(
    diamonds
    >> select(X.carat)
    >> head(2)
)
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
      <th>carat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
    </tr>
  </tbody>
</table>
</div>



## matplotlib


```python
import matplotlib.pylab as plt
```


```python
print(plt.style.available)
```

    ['seaborn-notebook', 'seaborn-deep', 'dark_background', 'classic', 'seaborn-talk', 'seaborn-whitegrid', 'seaborn-colorblind', 'seaborn-paper', '_classic_test', 'seaborn-ticks', 'fast', 'seaborn-bright', 'seaborn-pastel', 'ggplot', 'seaborn-white', 'seaborn', 'seaborn-dark-palette', 'seaborn-muted', 'grayscale', 'seaborn-darkgrid', 'Solarize_Light2', 'fivethirtyeight', 'bmh', 'tableau-colorblind10', 'seaborn-poster', 'seaborn-dark']



```python
plt.style.use('bmh')
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-945bcc9c98de> in <module>()
    ----> 1 plt.style.use('bmh')
    

    NameError: name 'plt' is not defined



```python
plt.style.use('tableau-colorblind10')
```


```python
plt.style.use('seaborn-poster')
```


```python
plt.style.use('dark_background')
```


```python
plt.style.use('classic')
```


```python
plt.style.use('seaborn-whitegrid')
```


```python
plt.style.use('seaborn-colorblind')
```


```python
plt.style.use('seaborn-deep')
```


```python
plt.style.use('seaborn-paper')
```


```python
plt.style.use('grayscale')
```


```python
plt.style.use('Solarize_Light2')
```


```python
plt.style.use('seaborn-dark')
```


```python
plt.style.use('ggplot')
```


```python
plot([1,2,3,9])
plt.grid(False)
show()
```


![png](P_dfply_with_diamond_files/P_dfply_with_diamond_229_0.png)



```python
plt.grid(False)
```


![png](P_dfply_with_diamond_files/P_dfply_with_diamond_230_0.png)



```python
plot_data = (
    diamonds
    >> select(everything())
#     >> head(10)
)

```


```python
plot_data.hist(bins=10)
plt.show()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-f1137bd6e689> in <module>()
    ----> 1 plot_data.hist(bins=10)
          2 plt.show()


    NameError: name 'plot_data' is not defined

