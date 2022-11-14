# NumPy [Basic](https://numpy.org/devdocs/user/absolute_beginners.html)
1. 거의 모든 과학 및 공학분야에서 사용되는 오픈소스 Python 라이브러리
2. 인터프리터 언어 (자바는 컴파일언어)
3. List보다 빠르고 컴팩트, 배열은 메모리를 덜 소모한다
## Array
1. `ndarray` = `N-dimensioanl Array`
2.  ![이미지](https://numpy.org/devdocs/_images/threefundamental.png)  
### 배열 만드는 법
1.  `np.array(object, dtype=None)`
2.  `np.zeros(shape, dtype=float)`
3.  `np.full(shape, fill_value, dtype=None)`
4.  `np.ones(hape, dtype=None)`
5.  `np.empty(shape, dtype=float)` --> _영역을 잡아서 제공하기 때문에 `zeros`와 `ones`보다는 속도가 빠름_
6.  `np.arange([start,] stop[, step,], dtype=None)`
7.  `np.linspace(start,stop,num=50,endpoint=True,retstep=False,dtype=None,axis=0)`

## sort
### np.sort(a, axis = -1)
### np.argsort(a, axis = -1)
