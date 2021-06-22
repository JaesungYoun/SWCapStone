# SWCapStone

# 소프트웨어융합캡스톤디자인 

## GSR(피부 전도도)를 이용한 머신러닝 기반 감정 분류 SW 개발

## 1. Introduction
과제 선정 배경
- 감정은 의사 결정, 지각 등에 직접적으로 영향을 미치며 인간의 삶에서 중요한 역할을 한다.
- 최근 인공지능 기술의 발달과 더불어 감정인식은 중요한 연구 분야로 대두되고 있음. 기존의 음성, 얼굴을 기반으로 한 감정 연구에서 더 나아가 최근에는 갈바니 피부 반응(GSR, Galvanic Skin Response), 심전도(ECG, electrocardiogram) 와 같은 생체신호를 활용하는 감정 연구로 확대되고 있다.
- GSR 센서를 사용하여 요가와 같은 정적 활동을 보다 잘 측정 할 수있는 웨어러블 플랫폼을 개발

### GSR
- 피부의 전기적 특성을 지속적으로 변화시키는 인체의 특성
- GSR 센서는 피부의 전기 전도도를 측정하여 심리적 각성의 척도를 제공함
- 과거 GSR은 심전도 (EKG)와 같은 의료 기술을 개발하는 데 사용되며 자율 신경계의 동정적인 활동과 관련된 땀샘 활동을 추적하여 심리적, 정서적, 생리적 각성과 동요를 감지하는 방법으로도 사용됨
- 실제로 GSR은 스트레스를받는 사람을 표시 할 수 있음
- GSR 측정 시 손가락이나 손목에 전극 두 개를 놓고 피부의 전도도를 측정


![image](https://user-images.githubusercontent.com/73388615/122944729-06b40580-d3b3-11eb-9478-5b4199bd5bd6.png)


### 감정 분류 방법
- Multi-class classification-
HAHV(High-Arousal,High-Valence), HALV(Hig
   Arousal,Low-Valence), LALV(Low-Arousal,Low- 
   Valence),LAHV(Low-Arousal,High-Valence) 4가지
   Label

- Binary classification
    - HA(High-Arousal), LA(Low-Arousal)
    - HV(High-Valence), LV(Low-Valence)  
    
    
![image](https://user-images.githubusercontent.com/73388615/122945330-7aeea900-d3b3-11eb-8d62-fe8ecf1f8539.png)


## 2. Data Analysis
### AMIGOS Dataset
- 1~40번 실험자 40명의 20개 Video에 대해 측정한 생체신호(EEG,ECG,GSR)를 128 HZ로 다운 샘플링된 신호
- 각 Video 마다 채널 17개로 구성 (EEG(14), ECG(2), GSR(1))
- 주관적 평가 방법에 의해 측정된 SA(Self-Assessment) 데이터셋
- 총 12개의 감정, 5개의 감정[1~9], 7개의 감정[0,1])을 Label로 활용

[arousal, valence, dominance, liking, familiarity] 0~9
   [neutral, disgust, happiness, surprise, anger, fear,
   sadness] 0,1 
- 각 Video의 17번 Channel에 해당하는 GSR 신호만 추출
- 신호 값 및 감정 평가 점수가 누락되어 있는 결측치 삭제 

### GSR Signal

Short Video 16 Long video 4

![image](https://user-images.githubusercontent.com/73388615/122945898-de78d680-d3b3-11eb-9a98-8e26eef66d94.png)

### Feature Extraction(Time Domain)
- Min 각 신호들의 최솟값 
- Max 각 신호들의 최댓값
- Mean 각 신호들의 평균
- STD 각 신호들의 표준편차
- Median 각 신호들의 중위값 
- Variance 각 신호들의 분산
- Skewness(왜도)
  - 분포의 비대칭성을 나타내는 척도
  - 특정 데이터의 분포 모양이 정규분포에서 어느 정도 벗어나있는지 알 수 있음
- Kurtosis(첨도)
   - 분포의 뾰족한 정도를 나타내는 척도
   - 특정 데이터의 분포 모양이 정규분포에서 어느 정도 벗어나있는지 알 수 있음
- Shannon Entropy(SE)
  - 신호의 Complexity를 반영해주는 Measure
- Log Energy Entropy(LEE)
  -  신호의 Complexity를 반영해주는 Measure
- Peak
  - 신호에서 나타나는 봉우리 수 

## 3. Classification

- 감정 중 Arousal, Valence 을 Label로 활용 
![image](https://user-images.githubusercontent.com/73388615/122946511-61019600-d3b4-11eb-9866-a47d94d56b22.png)

   - Arousal >= 5  High Arousal      
   - Arousal  <  5  Low Arousal
   - Valence >= 5  High Valence
   - Valence  < 5   Low Valence


### Multi-class Classification

- Linear SVM
     All of videos 

![image](https://user-images.githubusercontent.com/73388615/122946590-74acfc80-d3b4-11eb-9e93-479320036637.png)
     Only short video

![image](https://user-images.githubusercontent.com/73388615/122946672-868e9f80-d3b4-11eb-8055-15111d0c4af0.png)

- Random Forest
   All of videos 

![image](https://user-images.githubusercontent.com/73388615/122947099-dbcab100-d3b4-11eb-87bf-87442c06c0bc.png)

   Only short video 

![image](https://user-images.githubusercontent.com/73388615/122947064-d53c3980-d3b4-11eb-837c-a79a826f0258.png)



