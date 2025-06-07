# Spaceship Titanic

---

---

https://www.kaggle.com/competitions/spaceship-titanic

# Overview

Based on data, build a model that successfully predict the transported passengers

---

# Data

- Training data (train.csv)
- Testing data (test.csv)

## Data Dictionary

| Variable | Definition | Key |
| --- | --- | --- |
| PassengerId | Unique Id for each passenger | **gggg_pp**
**gggg** : group number
**pp** : number within the group |
| HomePlanet | Planet the passenger departed from |  |
| CryoSleep | Indicates whether the passenger is put to sleep, they get confined to their cabins | True/False |
| Cabin | Passenger’s cabin number. Takes from **deck/num/side**, where **side** can be either **P** for ***port*** or **S** for ***starboard*** | G/3/S |
| Destination | The planet the passnger is debarking to  |  |
| Age | The age of the passenger | Num |
| VIP | Whether the passenger has paid for special VIP service | True/False |
| RoomService/FoodCourt/ShoppingMall/Spa/VRDeck | The amount of money the passenger spent on each services | Num |
| Name | First & Last name |  |
| Transported | Whether the passenger was transported to another dimension (Target Val) |  |

## Submission Type

**submission.csv**

```cpp
PassengerId,Transported
0013_01,False
0018_01,False
0019_01,False
0021_01,False
etc.
```

- PassengerId - Id for each passenger in the test set
- Transported - The target, For each passenger, True/False

---

# Model

## 1st Submission

Base model : Random Forest

> **0.78746**
> 

## 2nd Submission

Random forest with ***parameter tweaks***

- n_estimators = 300 : 트리 개수, 많을수록 안정적이다
- max_dept = 12 : 최대 깊이, 과적합 방지에 도움
- min_samples_split = 4 : 노드 분할 위한 최소 샘플 수
- min_samples_leaf = 2 : 리프 노드에 있어야 하는 최소 샘플 수
- max_features = ‘sqrt’ : 각 노드 분할 시 고려할 feature 수
- class_weight = ‘balanced’ : 클래스 불균형 처리
- random_state = 42 : 결과 재현을 위한 시드

> **0.79074**
> 

## 3rd Submission

1. **Merge features**
    
    RoomService + FoodCourt + ShoppingMall + Spa + VRDeck = TotalSpending
    
2. **Split cabin**
    
    Split the cabin feature into three parts
    
3. **Get rid of anomalies**
    
    

> **0.75379**
> 

## 4th Submission

1. **Fix overfitting**
2. **Get rid of useless features**
3. **Normalization**

> **0.79822**
> 

## 5th Submission

- Base model : LightGBM
- Preprocessing
    - Cabin → Only use Deck, Side
    - TotalSpending + Log normalization
    - SpendingWhileAwake = Spendings while not in CyroSleep

> **0.80032**
> 

# Results

- Random Forest

| Base Model | 0.78746 |
| --- | --- |
| Parameter Tweak | 0.79074 |
| Feature Tweak | 0.75379 |
| Normalization | 0.79822 |
- LightGBM

| Base + Parameter | 0.80032 |
| --- | --- |