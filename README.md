# Trauma-Detector
# 트라우마 초기 진단을 위한 음성 기반 감정 분류 방법
Voice-based emotion classification for screening trauma

![image](https://img.shields.io/badge/language-C%23-blue?style=flat-square&logo=Visual-Studio)
![image](https://img.shields.io/badge/Latest%20Update-200405-9cf?style=flat-square)
![HitCount](http://hits.dwyl.com/minji-o-j/Trauma-Detector.svg)   



[데이터셋 & 데이터 전처리](#-데이터셋-&-데이터-전처리) 

[목적 및 필요성](#-목적-및-필요성) 

[개발자](#-개발자) 

[개발 기간](#-개발-기간)  

[사용 프로그램](#-사용-프로그램)  

---
## ◼ 데이터셋 & 데이터 전처리
- 국내 방송 영화 추출 데이터셋

  총 100명(남자 40명, 여자 60명), 2~11s 길이의 한국어 음성 데이터로 구성됨

  6가지 기본 감정(happy, sad, disgust, angry, surprise, fear)으로 구성됨

- 트라우마 감정 정의

  6가지 기본 감정 중 fear, sad를 트라우마를 가진 감정으로, neutral, happy를 트라우마가 아닌 감정으로 대체함

- 데이터 전처리

  ① 0.1s 단위로 shift하며 데이터를 2s단위로 자르기
  
  -> 데이터 간의 길이 차이를 없애고 데이터의 수를 늘림
  
  ② STFT(Short-time Fourier Transform Spectogram)

  STFT는 시계열 데이터를 일정 시간 구간으로 나눈 후, 해당 구간의 데이터를 푸리에 변환하는 방법
  
  2s 길이의 데이터를 sampling rate=1024로 설정해 FFT 수행->
  
  샘플 512개 만큼 오버랩하며 shift하도록 설정 -> min-max scaler를 사용해 스케일링 

  <img src="https://user-images.githubusercontent.com/33839093/92070141-425eee00-ede6-11ea-9965-fd350665224f.jpg" width="30%">


---
## ◼ 목적 및 필요성
트라우마에 대한 편견으로 인해 병원 방문을 꺼리는 사람들이 많고 자신이 가진 트라우마에 대해 스스로 인지하지 못해 진단과 치료를 놓지는 경우가 많다.

딥러닝은 공학기술, 의료분야와 결합되어 흉요추 골절, 안면 비대칭 등 다양한 분야에서 의사들의 초기 진단에 도움을 주고 있다.

음성 데이터를 활용한 성별 및 연령 분류, 음성 감정인식 등 활발한 연구가 진행되고 있으며 본 연구에서는 거부감이 없고 자연스러운 환경에서 비접촉식으로 얻을 수 있는 음성 데이터로 딥러닝 모델을 학습했다.

음성 데이터를 통해 트라우마의 초기 진단에 도움을 주는 시스템을 구축했다.

---
## ◼ 개발자

- [한나연(HanNayeoniee)](https://github.com/HanNayeoniee), [김나혜(nahye03)](https://github.com/nahye03), [김소의(DDoeuiGongju)](https://github.com/DDoeuiGongju), [목지원(mjw2705)](https://github.com/mjw2705), [유수경(sugyeong-yu)](https://github.com/sugyeong-yu)
---
## ◼ 개발 기간
- 2020/03 ~ 2020/08


---
## ◼ 사용 프로그램
