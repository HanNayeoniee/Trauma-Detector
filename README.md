# Trauma-Detector
# 트라우마 초기 진단을 위한 음성 기반 감정 분류

![image](https://img.shields.io/badge/language-python-blue?style=flat-square&logo=python)
![image](https://img.shields.io/badge/Latest%20Update-2020/09/17-9cf?style=flat-square)


## Authors

2020 국제차세대융합기술학회 트라우마 초기 진단을 위한 음성 기반 감정 분류 방법  (☞ﾟヮﾟ)☞ [논문 보러가기](https://drive.google.com/file/d/1Ch9q_fEED1EPn9OKLV89awkRNdj-LEB1/view?usp=sharing)

IHCI 2020 Screening Trauma Through CNN-Based Voice Emotion Classifiaction  (☞ﾟヮﾟ)☞ [논문 보러가기](https://drive.google.com/file/d/1OCGmmoeDsa8kCd8lgcxNivunHfMsDpuZ/view?usp=sharing)

|                 김나혜                |              김소의               |                 목지원                |              유수경               |                 한나연               |
| :------------------------------------------: | :-----------------------------------------: | :----------------------------------------: | :------------------------------------------: | :------------------------------------------: |
| <img src="https://user-images.githubusercontent.com/33839093/134200577-21e58590-1e1f-4890-85d9-b83a8edb8475.png" width=150px> | <img src="https://user-images.githubusercontent.com/33839093/134200749-613e54a4-cb1e-4fb6-8be6-b5204a1c6bff.png" width=150px> | <img src="https://user-images.githubusercontent.com/33839093/129562599-c27f52c9-31cc-4f25-916e-ce0dbee6f315.jpg" width=150px> | <img src="https://user-images.githubusercontent.com/33839093/134200983-9f034ef0-3b2f-4b18-8a2e-b09f7ae3c030.PNG" width=150px> | <img src="https://user-images.githubusercontent.com/33839093/129561824-7f779bf8-8036-4ab6-812e-4c7aa12c3d79.png" width=150px> |
|                   **[Github](https://github.com/nahye03)**                   |                   **[Github](https://github.com/DDoeuiGongju)**                   |               **[Github](https://github.com/mjw2705)**               |                   **[Github](https://github.com/sugyeong-yu)**                   |               **[Github](https://github.com/HanNayeoniee)**               |


## Approach
- 트라우마에 대한 편견으로 인해 병원 방문을 꺼리는 사람들이 많고 자신이 가진 트라우마에 대해 스스로 인지하지 못해 진단과 치료를 놓지는 경우가 많다.

- 음성 데이터를 활용한 성별 및 연령 분류, 음성 감정인식 등 활발한 연구가 진행되고 있으며 
본 연구에서는 거부감이 없고 자연스러운 환경에서 비접촉식으로 얻을 수 있는 음성 데이터로 딥러닝 모델을 학습했다.

- 음성 데이터를 통해 트라우마 초기 진단에 도움을 줄 수 있다.

## Dataset
- 국내 방송 영화 추출 데이터셋

  총 100명(남자 40명, 여자 60명), 2~11s 길이의 한국어 음성 데이터로 구성됨

  6가지 기본 감정(happy, sad, disgust, angry, surprise, fear)으로 구성됨

- 트라우마 감정 정의

  6가지 기본 감정(happy, sad, disgust, angry, surprise, fear) 중 fear, sad를 트라우마를 가진 감정으로, neutral, happy를 트라우마가 아닌 감정으로 대체함

## Pre-processing

  ① 음성을 0.1s 단위로 shift하며 2s 단위로 재구성
  
  -> 데이터 간의 길이 차이를 없애고 데이터의 수를 늘림
  
  ② STFT(Short-time Fourier Transform) 후 spectrogram 수행
  
  1차원 음성 데이터를 2차원 이미지로 변환함.

  STFT는 시계열 데이터를 일정 시간 구간으로 나눈 후, 해당 구간의 데이터를 푸리에 변환하는 방법
  
  2s 길이의 데이터를 sampling rate=1024로 설정해 FFT 수행 -> 샘플 512개 만큼 overlap하며 shift -> 
  모든 데이터가 0~1 사이의 값을 가지도록 min-max scaler를 사용해 스케일링 

  <img src="https://user-images.githubusercontent.com/33839093/134281938-8cc420b9-43f3-42b8-8de0-b55e6169956e.PNG" width=500px>

> 데이터 전처리 과정

  <img src="https://user-images.githubusercontent.com/33839093/134281998-7a6dddfd-a5c3-4573-b9b4-ea2d67a1398d.PNG" width=450px>

> 음성 데이터 스펙트로그램 예시
>
> (a) fear, (b) sad, (c) happy, (d) neutral에 해당하며 (a), (b)는 트라우마 감정, (c), (d)는 트라우마가 아닌 감정으로 사용 


## Model

> - VGG-13
>
> <img src="https://user-images.githubusercontent.com/33839093/134285303-77bd6ffc-7c6d-415f-bf9c-d1a1edaec982.PNG" width=400px>

> - VGG-16
>
> <img src="https://user-images.githubusercontent.com/33839093/134291073-6f5c5beb-0fad-4afd-ac84-5b395cbb54e5.png" width=400px>

> - VGG-19
> 
> <img src="https://user-images.githubusercontent.com/33839093/134291584-cdcd61c5-b12c-40f6-a3a1-93169f9ececb.png" width=350px>

## Post-processing

window size 크기 안의 예측값이 모두 1일 때 최종적으로 1로 예측하고, 모두 0일 때 0으로 예측한다. 

<img src="https://user-images.githubusercontent.com/33839093/137657118-d3cbb7ee-ef30-460c-8384-e9b49d7e51c5.PNG" width=350px>

> window size=4일 때 후처리를 통한 최종 예측값 :
>
> (1, 1, 1, 1) -> 1
>
> (1, 1, 1, 0) -> 1
>
> (1, 1, 0, 0) -> 1
>
> (1, 0, 0, 0) -> 1
>
> (0, 0, 0, 0) -> 0


## Accuracy

|Model|Test accuracy|
|---|---|
|VGG-13|98.96%|
|Layer-14|98.49%|
|VGG-16|96.42%|
|Resnet-50|87.35%|

<img src="https://user-images.githubusercontent.com/33839093/134285636-a4e23a95-53d5-4056-a957-00b0e6566906.PNG" width=300px>

> confusion matrix

<img src="https://user-images.githubusercontent.com/33839093/134285644-466b74f8-e775-4b70-bf52-d9127cfb5e00.PNG" width=300px>

> ROC curve

## Files
- [pre-processing.ipynb](https://github.com/HanNayeoniee/Trauma-Detector/blob/master/pre-processing.ipynb) : 음성 데이터 전처리
- [VGG_train_test.ipynb](https://github.com/HanNayeoniee/Trauma-Detector/blob/master/VGG_train_test.ipynb) : VGG모델 학습 및 성능 평가

## Installation
```python
(git bash)
git clone https://github.com/HanNayeoniee/Trauma-Detector.git

(anaconda prompt)
pip install -r requirements.txt
```