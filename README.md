# 클래식 입문자를 위한 예술의전당 좌석 별 관람 포인트 안내도
## 1. 배경
### 클래식 입문자의 좌석 선택 딜레마 : 경험 부재와 예술의전당 가격정책의 한계

#### 1)	현장 경험 부재에 기인한 클래식 입문자의 좌석 선택 고민
처음 클래식 공연을 감상하는 관객들은 실제 현장에서 관람해본 경험이 없기 때문에 좌석에 대한 주관적인 선호도가 존재하지 않는다. 따라서 클래식 입문자들은 예술의 전당에서 표를 예매하기 위해 좌석을 선택할 때, 어떤 좌석이 해당 공연에 가장 적합한지 모르기 때문에 혼란을 느낀다.

#### 2)	좌석에 대한 정보를 제공하지 못하고 있는 현재 예술의전당의 가격 모델
클래식을 즐기는 매니아 층에 의하면 클래식은 장르에 따라 연주자의 손이 잘 보이는 자리, 소리의 울림이 좋은 자리 등으로 원하는 좌석이 달라진다고 한다. 그러나 현재 예술의전당의 가격 모델은 좌석에 대한 정보를 제공하고 있지 못한다. R석의 가격이 가장 높지만, 이는 가장 인기 있는 좌석을 의미하는 것이 아니며, 클래식을 현장에서 관람한 경험이 적은 입문자는 비싼 좌석이 좋은 좌석일 것이라는 인식이 있기 때문에 R석을 우선적으로 선택하게 된다. 이러한 혼란은 관객이 실제로 인기있는 좌석을 선택하지 못해 합리적으로 좌석을 결정할 수 없게 만든다. 공연에 대한 만족도 저하로 이어져 장기적으로는 클래식홀의 만족도 저하로 이어질 수 있다.


## 2. 목적 및 필요성
클래식 공연은 그 특성 상, 동일한 공연장 내에서도 장르와 좌석 위치에 따라 관객이 느끼는 음향과 시야가 크게 변화한다. 이러한 다양한 조건에 따라 각 관객이 선호하는 좌석이 달라지게 되는데, 이를 고려하여 좌석의 가격을 조절하는 것이 필요하다는 점이 부각된다. 그러나, 공연예술은 관객이 직접 경험하기 전까지 그 가치를 정확히 평가하기 어려운 경험재의 특성을 가지고 있다. 이에 따라 유사한 공연의 정보를 통해 그 공연의 가치를 추정하고, 예측하기 힘든 리스크 요인을 최소화하는 방안을 찾아야 한다. <br>
이 문제의 해결책으로 각 좌석의 관람 포인트, 시야, 그리고 고객별 관람 성향을 종합적으로 반영하여 공연의 가치를 예측한다. 이를 통해 클래식 입문자들에게 "예술의전당 좌석 별 관람 포인트 안내도"를 제공함으로써 관객의 만족도를 높이고 공연장의 수익도 극대화할 수 있는 방안을 제시한다.

## 3. 분석 수행 절차
<img width="1449" alt="스크린샷 2023-09-28 오전 9 28 04" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/e9ca41ac-5a49-4ea0-a286-43df1e8e3c1c">

### 1) 인기좌석 라벨링
연주자의 손이 잘 보이는 좌석, 음향이 입체적인 좌석, 전반적인 시야가 좋은 좌석 등 장르 별로 인기 있는 좌석 라벨링 <br>

![008](https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/a00592ed-5766-4944-a9d7-b86103eb3ec9)

### 2) 좌석 클러스터링
- 각 장르별로 좌석의 특성과 인기도가 다르다는 것을 확인한 후, 장르마다 개별적으로 클러스터링을 수행하기로 결정 <br>
- 공연 별 총 예매수, 총 매출, 취소된 예매 수 등을 고려해 좌석 그룹핑 가설을 수립하고 공연 K-means, DBSCAN 클러스터링
<img width="476" alt="image" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/570753a1-0bea-4fb2-aff1-00ea3718576f">

### 3) 가격 모델링
#### A. 좌석예매비율 예측 변수 생성
- 공연기획 시 기획정보(공연명 W2V 변수, 운영할 좌석 등급 수, 공연시간 대비 쉬는 시간 등)를 input하면 공연 기대수익을 달성할 수 있는 클러스터별 중요도에 맞는 차등된 가격을 알아내도록 클러스터별 좌석예매비율을 예측하도록 설정
<img width="1638" alt="스크린샷 2023-09-28 오전 9 39 43" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/f1a7c518-49e8-4817-a3d7-83871d957270">

- 클러스터별 특징을 반영하기 위해 공연일자 순으로 정렬한 상태에서 이전 공연들의 관람 포인트 좌석예매 수 산술평균, 최근 2개 공연의 관람 포인트 좌석예매 수 이동평균 등을 변수로 사용.

  <img width="1626" alt="스크린샷 2023-09-28 오전 9 42 57" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/5d762f13-1ede-434a-833d-21623457191b">
  
-  이후 장르마다 TabNet을 학습시키고 중요하지 않은 변수를 제거하는 과정을 반복해 유의한 변수만을 사용한 TabNet 모델을 만듬


## 4. 결과
### 1) 좌석 클러스터링 예시
##### [클러스터 1 : 밸런스 오디오석 (Balance Audio Seat)]  
•	예매율(booking_rate): 약 51%  
•	예매 시간(res_time_rank_mean): 매우 빠름 (0.57)  
•	좌석 위치 : 대부분 1층 에 분포(약 99%)  
•	특이사항: 공연장 중앙에 위치하여 모든 악기군을 군형 있게 들을 수 있으며 공간 음향이 잘 조화되어 전체적인 음질이 뛰어남   

##### [클러스터 2 : 다이나믹 뷰석 (Dynamic View Seat)]   
•	예매율(booking_rate): 약 21%  
•	예매 시간(res_time_rank_mean): 빠르지 않음 (0.42)  
•	좌석 위치 : 합창석  
•	특이사항 : 합창석은 고른 소리를 듣기 어려운 단점이 있지만 지휘자와 연주자의 모습을 코앞에서 볼 수 있다.    

##### [클러스터 3 : 베스트 인기석 (Most Popular Seat)]   
•	예매율(booking_rate): 약 90%  
•	예매 시간(res_time_rank_mean): 매우 빠름 (0.68)       
•	좌석 위치: 1층 A블록 15열 / B블록,C블록 통로 좌석    
•	특이사항 : 1층 A블록 15열은 '발을 뻗을 수 있는 좌석'으로 편안하게 공연을 즐길 수 있으며 B블록,C블록 통로 좌석은 공연자의 제스쳐를 섬세히 관찰할 수 있음     
 
##### [클러스터 4 : 사이드 오프석 (Side Off Seat)]   
•	예매율(booking_rate): 약 40%
•	예매 시간(res_time_rank_mean): 느림 (0.3)  
•	좌석 위치 : 2층 사이드 좌석 / BOX석 / 3층   
•	특이사항 : 음향이 덜 도달할 뿐만 아니라 연주자의 표정이나 지휘자의 동작 등을 자세히 볼 수 없다. 또한 박스석은 시야방해석으로, 공연을 잘 조망하기 어렵다
![015](https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/43b2519a-0273-4ebd-af36-a38cfdfedad3)
![016](https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/eaaa69db-0571-4041-adad-705a9be4542b)

### 2) 가격 모델링 결과
<img width="1164" alt="스크린샷 2023-09-28 오전 9 44 27" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/41396317-3984-4584-994e-9012ac3c90ad">

## 5. 기대효과
<img width="1619" alt="스크린샷 2023-09-28 오전 9 51 36" src="https://github.com/HyunJiLee34/2023_Bigcontest/assets/79692017/3e6cc341-d844-44a4-aead-47804f51c22e">





