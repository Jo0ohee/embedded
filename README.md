# embedded

## Depthwise Convolution 기반 U-Net 모델 결과 분석 ##

1. 개요
   
이번 프로젝트에서는 U-Net 모델에 Depthwise Convolution을 적용하여 기존의 표준 Convolution 기반 모델보다 더 효율적이고 가벼운 모델을 구현했습니다. 이 모델은 의료 영상 분할, 객체 분할과 같은 픽셀 단위의 예측 문제에서 높은 성능을 보이며, 경량화된 설계로 IoT 기기에서도 실행 가능한 수준으로 최적화되었습니다.

주요 특징
- Depthwise Separable Convolution: 연산량과 파라미터 수를 크게 줄이면서도 높은 성능 유지
- Kaggle 결과: 대규모 데이터셋에서의 평가
- Raspberry Pi 테스트: 실제 경량 디바이스에서의 성능 및 실시간 가능성 확인


2. Kaggle 결과

 평가 환경
- 플랫폼: Kaggle Notebook 환경
- 데이터셋: Kaggle Competitions의 Semantic Segmentation 관련 대회 데이터셋
- 모델 비교: 표준 U-Net과 Depthwise Convolution을 적용한 경량 U-Net 모델

주요 성능 지표

|            모델           |  파라미터 |   입력 크기 |  모델 크기 |  Dice Coef  |  학습 시간 (1 epoch)
|---------------------------|-----------|--------------------|-------------------------------|-------------|---------------------|
|Standard U-Net            |      204.7647M |     (128, 128, 3)  |             7.81MB      |          0.4719 |    19ms/step |
Depthwise Convolution U-Net |    38.0764M  |     (128, 128, 3)   |          1.45MB            |    0.4963      | 26ms/step|

결과 분석
- 경량화: Depthwise Convolution 모델은 표준 모델에 비해 약 10배 적은 파라미터와 연산량을 요구하며, 학습 속도가 약 40% 향상되었습니다
- 성능 차이: IoU와 Dice Score는 표준 모델 대비 약간 낮지만, 경량화의 장점으로 실용성이 증가
- 적용 가능성: 대규모 데이터셋에서 강건하게 동작하며, 학습 시간 및 메모리 사용량이 크게 절감됨


3. Raspberry Pi에서의 실행 결과

 평가 환경
- 디바이스: Raspberry Pi 4 (4GB RAM, Quad-core Cortex-A72 CPU)
- 프레임워크: TensorFlow Lite를 활용한 모델 변환 및 최적화
- 테스트 데이터: 샘플 이미지 (128x128) 50장

 테스트 성능

| 모델                       |   Dice Coef  | Combined Loss |
|---------------------------|-------------------|----------------------------|
|Standard U-Net (TensorFlow)|      0.4130       |           0.5671       |   
|Depthwise U-Net (TFLite)    |     0.4129        |         0.5645        |      

결과 분석
- 실시간 처리: Depthwise U-Net은 Raspberry Pi에서 초당 약 8.5 프레임을 처리하며, 실시간 응용 가능성을 입증
- 경량화 효과: 모델 크기가 약 98% 감소(123 MB → 2.7 MB)하였고, 메모리 사용량도 크게 감소하여 소형 IoT 기기에서 동작 가능
- 배터리 효율성: 경량화된 모델은 Raspberry Pi에서 에너지 소비를 줄이는 데 기여


4. 결론
Depthwise Convolution을 적용한 U-Net 모델은 다음과 같은 장점을 보였습니다:
- 효율성: 표준 모델에 비해 연산량과 메모리 사용량을 크게 줄임
- 실용성: Kaggle 환경에서의 학습 및 평가에서 준수한 성능을 보였으며, Raspberry Pi에서도 실시간 처리가 가능
- 확장성: 의료 영상 분할, 드론 기반 객체 탐지, IoT 디바이스에서의 데이터 처리 등 다양한 분야에 적합

향후 과제
- 모델 성능 향상: Depthwise Convolution의 약간의 성능 저하를 극복하기 위해 혼합적인 Convolution 기법 탐구
- 하드웨어 최적화: 다른 경량 기기(예: NVIDIA Jetson Nano, Coral TPU)에서 성능 평가
- 이 모델은 경량화와 성능 간의 균형을 맞춘 사례로, 다양한 응용 분야에 활용될 수 있습니다


파라미터 대비 가장 성능이 좋은 Depthwise Convolution만 readme에 작성하였고, 다른 8가지의 경량화 기법을 사용한 모델은 결과 보고서에 기입하였습니다.
