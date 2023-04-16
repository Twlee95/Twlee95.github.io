---
title:  "[Kaggle] competition 참가방법과, 시작방법"
excerpt: "kaggle 시작"

categories: [Kaggle, Tutorial]
tags:
  - [Kaggle, competition, Github, Git, Blog]

toc: true
toc_sticky: true
 
date: 2022-01-21
last_modified_at: 2022-01-21
---

# OVERVIEW OF KAGGLE

1. 대회가 어떤 주제인지 Description
2. Data의 종류와 분량 확인 (EDA)
3. Evaluation metric 확인 + 리더보트 대략 확인 
4. 기존에 논의된 Discussion 살펴보기
5. Upvote 많은 Notebook 살펴보기


## FOR LARGE DATASETS
 - Dask
 - Datatable
 - Rapids (cudf)
  (boosting 사용시 cuml 등 을 사용하여 gpu 사용)

## 다양한 데이터셋 활용
 - Spicy :과학 계산용 library
 - librosa : 음성 처리 라이브러리
 - Pillow, skimage, imageio : 이미지용 라이브러리

## visualization
 - Matplotlib
 - seaborn
 - Plotly
 - 수많은 시각화 방법과 라이브러리

## EDA시각화의 4가지. (정보 시각화)
1. Composition (구성)
  - 34 percent of this data is woman
2. Distribution (분포)
  - what is specific shape of each variables
3. relationship (관계)
  - relationship of each feature
4. compareison (비교)
     

## 왜 f1 score를 쓸까?
 - 데이터의 분포에 따라 accuracy가 필요가 없어지는 경우가 있다.


## Competition scoreboard    
  
  - public : 대회 중간 score  
  - private : 대회 최종 socre  
  
  test Dataset의 score에 overfitting되는 일을 방지하기 위한 장치  
  public이 높다고 최종 Private까지 좋지는 않다!    
  제출 파일을 2개 선택하는데, 잘 선택해야함(overfitting과의 싸움) 


## 머신러닝 적용 3요소

1. 개념적 이해  
모델은 어떤 아이디어를 가지고 있을까?  
기존 모델의 어떤 점을 개선했을까?  
이 모델의 장단점은 무엇일까?  
무엇을 계산하고 있는걸까?

2. 프로그래밍 스킬
라이브러리, 모델구현,   
모델 커스텀, 시간과 컴퓨팅 코스트 줄이기  
재사용성과 가독성

3. 수학 + 도메인 지식  
모델 내부에는 어떤 과정이 진행될까?  
데이터는 어떻게 살펴볼까?  
데이터에 따른 전처리방법  
데이터에서 노이즈 확인  
가정을 어떻게 검증할까?  

###  남의 노트북 뺏어 쓰기
-> copy and edit notebook


#  실습
## 데이터 불러오기 및 데이터 정보 확인
```
train = pd.read_csv('/kaggle/input/asdasdasd')
train.head()
train.columns # 변수 이름 등
train.info() ## 데이터프레임의 데이터 형태, Null 확인 

## 결측 데이터 시각화 확인
import missingno as msno
msno.martix(train)

train['asdasd'].value_counts()



## 0 or 1 로 바꿔주면 피벗테이블 그릴 수 있다.
train['income'] = (train['income'] ==  '>50K').astype(int)

# grouby 를 사용해도 범주별로 좋음
train.groupby(['race','sex'])[['income']].mean().style.background_gradient(cmap="Purples")
# or
pd.pivot_table(train,
              columns='sex',
               index = 'race',
               values = 'income',
               aggfunc = 'mean')

## line plot
sns.kdeplot(data =train, x = 'age')
```


## 결과제출
```
from sklearn.tree import DecisionTreeClassifier
dt_clf = DecisionTreeClassifier()
dt_clf.fit(train_le, target)

dt_clf.predict(text_le)
->> array([0,0,0, ... ,0,0,0]) 


## 위에서 예측해준 값들을 sample_submission의 prediction 변수에 저장해줌
sample_submission['prediction'] = dt_clf.predcit(test_le).astype(int)
sample_submission.to_csv('submission.csv',index = False)
```

-> save vesrsion -> save & run
-> 내 결과는 output에 존재하는데, submit 눌러주면 됨
