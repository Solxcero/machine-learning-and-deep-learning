# NumPy [Basic](https://numpy.org/devdocs/user/absolute_beginners.html)
1. 거의 모든 과학 및 공학분야에서 사용되는 오픈소스 Python 라이브러리
2. 인터프리터 언어 (자바는 컴파일언어)
3. List보다 빠르고 컴팩트, 배열은 메모리를 덜 소모한다

<details>
<summary> <h2>Array </summary>
<div markdown="1">

1. `ndarray` = `N-dimensioanl Array`  

 ![이미지](https://numpy.org/devdocs/_images/threefundamental.png)  
### 배열 만드는 법
1.  `np.array(object, dtype=None)`
2.  `np.zeros(shape, dtype=float)`
3.  `np.full(shape, fill_value, dtype=None)`
4.  `np.ones(hape, dtype=None)`
5.  `np.empty(shape, dtype=float)` --> _영역을 잡아서 제공하기 때문에 `zeros`와 `ones`보다는 속도가 빠름_
6.  `np.arange([start,] stop[, step,], dtype=None)`
7.  `np.linspace(start,stop,num=50,endpoint=True,retstep=False,dtype=None,axis=0)`
    > start 부터  stop 까지 균등하게 num 등분하기 
</div>
</details>
<details>
<summary> <h2> sort </summary>
<div markdown="1">

### np.sort(a, axis = -1)
```python
>> a = np.array([[1,4],[3,1]])
>> np.sort(a)                # sort along the last axis
array([[1, 4],
       [1, 3]])
>> np.sort(a, axis=None)     # sort the flattened array
array([1, 1, 3, 4])
>> np.sort(a, axis=0)        # sort along the first axis
array([[1, 1],
       [3, 4]])
```

🧐추가로 
```python
>> dtype = [('name', 'S10'), ('height', float), ('age', int)]
>> values = [('Arthur', 1.8, 41), ('Lancelot', 1.9, 38),
          ('Galahad', 1.7, 38)]
>> a = np.array(values, dtype=dtype)       # create a structured array
>> np.sort(a, order='height')                        
array([('Galahad', 1.7, 38), ('Arthur', 1.8, 41),
       ('Lancelot', 1.8999999999999999, 38)],
      dtype=[('name', '|S10'), ('height', '<f8'), ('age', '<i4')])

>> np.sort(a, order=['age', 'height'])               
array([('Galahad', 1.7, 38), ('Lancelot', 1.8999999999999999, 38),
       ('Arthur', 1.8, 41)],
      dtype=[('name', '|S10'), ('height', '<f8'), ('age', '<i4')])
```
### np.argsort(a, axis = -1)
1차원 배열
```python
>> x = np.array([3, 1, 2])
>> np.argsort(x)
array([1, 2, 0])
```
2차원 배열
```python
>> x = np.array([[0, 3], [2, 2]])
>> x
array([[0, 3],
       [2, 2]])

>> ind = np.argsort(x, axis=0)  # sorts along first axis (down)
>> ind
array([[0, 1],
       [1, 0]])
>> np.take_along_axis(x, ind, axis=0)  # same as np.sort(x, axis=0)
array([[0, 2],
       [2, 3]])

>> ind = np.argsort(x, axis=1)  # sorts along last axis (across)
>> ind
array([[0, 1],
       [0, 1]])
>> np.take_along_axis(x, ind, axis=1)  # same as np.sort(x, axis=1)
array([[0, 3],
       [2, 2]])
```
</div>
</details>

<details>
<summary> <h2> np.concatenate() </summary>
<div markdown="1">

```python
>> a = np.array([1, 2, 3, 4])
>> b = np.array([5, 6, 7, 8])

>> np.concatenate((a, b))
array([1, 2, 3, 4, 5, 6, 7, 8])
```
```python
>> x = np.array([[1, 2], [3, 4]])
>> y = np.array([[5, 6]])

>> np.concatenate((x, y), axis=0)
array([[1, 2],
       [3, 4],
       [5, 6]])
```
⁉ 3차원
```python
>> a = np.array([[[1,2,3,4]]])
>> b = np.array([[[5,6,7,8]]])

>> np.concatenate((a,b),axis=0)
array([[[1, 2, 3, 4]],

       [[5, 6, 7, 8]]])

>> np.concatenate((a,b),axis=1)
array([[[1, 2, 3, 4],
        [5, 6, 7, 8]]])
```
</div>
</details>
<details>
<summary> <h2> 구조 파악하기  </summary>
<div markdown="1">

`a.ndim` : 배열의 차원   
`a.shape` : 배열의 모양
`a.size` :  배열에 있는 데이터 크기 
```python
>> a = np.array([[[1,2,3,4]]])
>> b = np.array([[[5,6,7,8]]])

#메서드 체이닝
print(np.concatenate((a,b),axis=0).size) # 8 
print(np.concatenate((a,b),axis=0).shape) # (2,1,4)
print(np.concatenate((a,b),axis=0).ndim) # 3
```
</div>
</details>
<details>
<summary> <h2> reshape  </summary>
<div markdown="1">

```python
>> a = np.arange(6)
>> a
array([0, 1, 2, 3, 4, 5])

>> a.reshape(3,2)
array([[0, 1],
       [2, 3],
       [4, 5]])

>> np.reshape(a,(2,3))
array([[0, 1, 2],
       [3, 4, 5]])
```
</div>
</details>
<details>
<summary> <h2> newaxis</summary>
<div markdown="1">

- 축 추가하기(=차원 늘리기)
```python
>> a = np.array([1,2,3,4,5,6])
>> a.shape
(6,)

>> a2 = a[np.newaxis,:]
>> print(a2) 
[[1 2 3 4 5 6]]
>> print(a2.shape)
(1, 6)

>> a3 = a[:,np.newaxis]
>> print(a3)
[[1]
 [2]
 [3]
 [4]
 [5]
 [6]] 
 >> print(a3.shape)
 (6, 1)
 ```
 </div>
 </details>
<details>
<summary> <h2> 기본 연산</summary>
<div markdown="1">

<p align='center'>
<img src="https://numpy.org/devdocs/_images/np_data_plus_ones.png" width="60%" /><br>
더하기 연산<br>
<img src="https://numpy.org/devdocs/_images/np_sub_mult_divide.png" width="60%" /><br>   
빼기 연산 / 곱하기 연산 / 나누기 연산 
</p>

### sum
```python
>> x = np.array([[1, 1], [2, 2]])
>> b.sum(axis=0)
array([3, 3])

>> b.sum(axis=1)
array([2, 4])
```

[기본 연산 더 알아보기☝](https://numpy.org/devdocs/user/quickstart.html#quickstart-basic-operations)
 </div>
 </details>
 <details>
<summary> <h2> Broadcasting </summary>
<div markdown="1">

- 두 개의 서로 다른 크기의 배열 간에 연산을 수행하려는 경우 
```python
>> data = np.array([1.0, 2.0])
>> data * 1.6
array([1.6, 3.2])
```
<!-- ![이미지](https://numpy.org/devdocs/_images/np_multiply_broadcasting.png) -->
<img src="https://numpy.org/devdocs/_images/np_multiply_broadcasting.png" width="60%"  />  

#### broadcast 충족 조건
1. they are equal(서로 같거나), or
2. one of them is 1(둘 중 하나가 1일 때 ).
[broadcast 자세히 알아보기🔎](https://numpy.org/devdocs/user/basics.broadcasting.html#basics-broadcasting)
</div>
 </details>
 <details>
<summary> <h2> 그외 </summary>
<div markdown="1">

### 난수 생성
```python
>> rng = np.random.default_rng(1) # 괄화 안에  seed 값 ( 머신러닝  random_state 값)
>> rng.random(3)
array([0.51182162, 0.9504637 , 0.14415961])

>> rng.integers(5,size=(2,4),endpoint=True) # endpoint : 5 를 포함시킬것인지 말것인지
array([[5, 3, 4, 1],
       [2, 4, 0, 1]], dtype=int64)
```
### unique
```python
>> a = np.array([11, 11, 12, 13, 14, 15, 16, 17, 12, 13, 11, 14, 18, 19, 20])

>> print(np.unique(a, return_index=True))
(array([11, 12, 13, 14, 15, 16, 17, 18, 19, 20]), array([ 0,  2,  3,  4,  5,  6,  7, 12, 13, 14], dtype=int64))

>> print(np.unique(a, return_index=False, return_inverse=True))
(array([11, 12, 13, 14, 15, 16, 17, 18, 19, 20]), array([0, 0, 1, 2, 3, 4, 5, 6, 1, 2, 0, 3, 7, 8, 9], dtype=int64))

>> print(np.unique(a, return_index=False, return_inverse=False,return_counts=True))
(array([11, 12, 13, 14, 15, 16, 17, 18, 19, 20]), array([3, 2, 2, 2, 1, 1, 1, 1, 1, 1], dtype=int64))
```
### transpose & T
```python
>> data = np.arange(6).reshape((2,3))
>> data.transpose()
array([[0, 3],
       [1, 4],
       [2, 5]])
>> data.T
array([[0, 3],
       [1, 4],
       [2, 5]])
```
### filp
```python
>> arr = np.array([1,2,3,4,9,6,7,8])
>> np.flip(arr)
array([8, 7, 6, 9, 4, 3, 2, 1])

>> arr_2d = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
>> print(arr_2d)
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])

>> print(np.flip(arr_2d))
[[12 11 10  9]
 [ 8  7  6  5]
 [ 4  3  2  1]] 

>> print(np.flip(arr_2d,axis=0))
[[ 9 10 11 12]
 [ 5  6  7  8]
 [ 1  2  3  4]] 

>> print(np.flip(arr_2d,axis=1))
[[ 4  3  2  1]
 [ 8  7  6  5]
 [12 11 10  9]]
```
### flatten & ravel
1. ravel은 복사본을 생성하지 않아 메모리 측면에서 효율적
2. copy는 깊은 복사, ravel 은 얕은 복사
```python
>> x = np.array([[1 , 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
>> print(x)
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]] 

>> print(x.flatten()) # x.reshape((1,-1))[0]과 동일한 결과. reshape는 차원을 고려해야 함
[ 1  2  3  4  5  6  7  8  9 10 11 12]
```
### Docstring 접근
1. `.속성명?` or  `x.속성명??`
2. *shift* + *tab* 으로 보는 게 더 편하다
```python
def double(a):
    '''
    여기에 함수 설명 쓰기 
    double(arr) 
    '''
    return a*2
```
```python
>> double?
Signature: double(a)
Docstring:
여기에 함수 설명 쓰기 
double(arr) 
File:      c:\users\user\appdata\local\temp\ipykernel_5372\2325553044.py
Type:      function

>> double?? # 소스 코드 같이 보여줌 
Signature: double(a)
Source:   
def double(a):
    '''
    여기에 함수 설명 쓰기 
    double(arr) 
    '''
    return a*2
File:      c:\users\user\appdata\local\temp\ipykernel_5372\2325553044.py
Type:      function
```
</div>
</details>
