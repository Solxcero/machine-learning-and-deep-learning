# NumPy [Basic](https://numpy.org/devdocs/user/absolute_beginners.html)
1. 거의 모든 과학 및 공학분야에서 사용되는 오픈소스 Python 라이브러리
2. 인터프리터 언어 (자바는 컴파일언어)
3. List보다 빠르고 컴팩트, 배열은 메모리를 덜 소모한다
## Array
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

## sort
### np.sort(a, axis = -1)
```
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
```
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
```
>> x = np.array([3, 1, 2])
>> np.argsort(x)
array([1, 2, 0])
```
2차원 배열
```
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
##  np.concatenate()
```
>> a = np.array([1, 2, 3, 4])
>> b = np.array([5, 6, 7, 8])

>> np.concatenate((a, b))
array([1, 2, 3, 4, 5, 6, 7, 8])
```
```
>> x = np.array([[1, 2], [3, 4]])
>> y = np.array([[5, 6]])

>> np.concatenate((x, y), axis=0)
array([[1, 2],
       [3, 4],
       [5, 6]])
```
⁉ 3차원
```
>> a = np.array([[[1,2,3,4]]])
>> b = np.array([[[5,6,7,8]]])

>> np.concatenate((a,b),axis=0)
array([[[1, 2, 3, 4]],

       [[5, 6, 7, 8]]])

>> np.concatenate((a,b),axis=1)
array([[[1, 2, 3, 4],
        [5, 6, 7, 8]]])
```
## 구조 파악하기 
`a.ndim` : 배열의 차원   
`a.shape` : 배열의 모양
`a.size` :  배열에 있는 데이터 크기 
```
>> a = np.array([[[1,2,3,4]]])
>> b = np.array([[[5,6,7,8]]])

#메서드 체이닝
print(np.concatenate((a,b),axis=0).size) # 8 
print(np.concatenate((a,b),axis=0).shape) # (2,1,4)
print(np.concatenate((a,b),axis=0).ndim) # 3
```
