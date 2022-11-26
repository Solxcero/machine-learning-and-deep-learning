## 📘 MachineLearning with Python

### Supervised Learning 🤖

#### 분류 / 회귀
+ 분류(Classification)는 미리 정의된, 가능성 있는 여러 클래스 레이블(class label) 중 하나를 예측하는 것. 이진분류(binary)는 두 개의 클래스로 분류. 다중분류(multiclass)는 셋 이상의 클래스로 분류
+ 이진분류에서 한 클래스를 양성(positive)클래스, 다른 하나를 음성(negative)클래스라고도 함. 양성클래스는 학습하고자 하는 대상을 의미. (스팸메일, 주관적으로 정의됨)
+ 회귀는 연속적인 숫자, 부동소수점수를 예측하는 것. 예상 출력값에 연속성이 있다면 회귀문제.

#### 일반화/과대적합/과소적합
가진 정보를 모두 사용해서 너무 복잡한 모델을 만들면 과대적합  → 모델이 훈련세트의 각 샘플에 너무 가깝게 맞춰져서 새로운 데이터에 일반화되기 어려움  
모델이 너무 간단하면 데이터의 면면과 다양성을 잡아내지 못하면 과소적합  
데이터셋에 다양한 데이터 포인트가 많을수록 과대적합 없이 더 복잡한 모델을 만들 수 있음.   
**우리가 찾아야하는 모델은 일반화 성능이 최대가 되는 최적점에 있는 모델**

<p align="center">
<img src="https://tensorflowkorea.files.wordpress.com/2017/06/fig2-01.png" width=300>
</p>

 

#### `UploadList`
1. KNN
2. LinearModel
3. DecisionTree
4. Ensemble

------------------------------------------------
### Unsupervised Learning 🎮
