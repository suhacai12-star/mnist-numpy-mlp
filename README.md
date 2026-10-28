# mnist-numpy-mlp
MNIST 손글씨 데이터셋을 활용해 NumPy로 신경망을 직접 구현하고, 학습 결과와 오분류 이미지를 분석하는 프로젝트
## Dataset

This project uses the MNIST handwritten digit dataset, loaded through `tensorflow.keras.datasets`.

- **Dataset:** MNIST handwritten digit dataset
- **Source:** [Keras MNIST Dataset Documentation](https://keras.io/api/datasets/mnist/)
- **Description:** 60,000 training images and 10,000 test images of handwritten digits (0–9).

The dataset is loaded using TensorFlow/Keras. The neural network architecture, forward propagation, backpropagation, and training process are implemented using NumPy.

The dataset itself is not included in this repository; it is downloaded through the dataset-loading function when needed.
# NumPy로 직접 구현한 MNIST MLP

## 프로젝트 소개

NumPy를 사용하여 다층 퍼셉트론(MLP, Multilayer Perceptron)을 구현하고, MNIST 손글씨 숫자 데이터셋을 이용해 숫자 분류를 수행하는 프로젝트입니다.

딥러닝 모델의 내부 동작 원리를 이해하는 것을 목표로, 딥러닝 프레임워크를 사용하지 않고 순전파(Forward Propagation), 역전파(Backpropagation), 학습 과정을 직접 구현했습니다.

TensorFlow/Keras는 MNIST 데이터셋을 불러오는 용도로만 사용했습니다.

## 주요 구현 내용

- NumPy를 이용한 순전파 구현
- 역전파 및 가중치 업데이트 구현
- Sigmoid, ReLU, Softmax 활성화 함수 구현
- Categorical Cross-Entropy 손실 함수 구현
- 미니배치(Mini-batch) 학습 구현
- 학습률에 따른 학습 과정 비교
- 테스트 데이터셋을 이용한 분류 정확도 평가
- 오분류 이미지 분석을 통한 모델의 한계 확인

## 모델 구조

모델은 총 3개의 완전연결층(Fully Connected Layer)으로 구성됩니다.

| 계층 | 차원 | 활성화 함수 |
|---|---:|---|
| 입력층 | 784 | - |
| 은닉층 1 | 512 | Sigmoid |
| 은닉층 2 | 128 | ReLU |
| 출력층 | 10 | Softmax |

MNIST 이미지는 28×28 크기의 흑백 이미지이며, 이를 784차원의 벡터로 변환하여 입력으로 사용합니다.

출력층은 0부터 9까지 총 10개의 숫자 클래스에 대한 예측값을 출력합니다.

## 학습 설정

- **데이터셋:** MNIST
- **모델 구현:** NumPy
- **데이터 로딩:** TensorFlow/Keras
- **손실 함수:** Categorical Cross-Entropy
- **배치 크기:** 100
- **에포크:** 40

## 실험 결과

학습률을 변경하며 모델의 학습 과정과 최종 분류 정확도를 비교했습니다.

| 학습률 | 테스트 정확도 |
|---:|---:|
| 0.1 | 약 93% |
| 0.01 | 약 97% |

실험 결과, 학습률 설정에 따라 학습 과정과 최종 성능에 차이가 나타났습니다.

### 오분류 이미지 분석

모델이 잘못 분류한 이미지를 확인한 결과, 다음과 같은 특징이 관찰되었습니다.

- **이미지의 블러 현상:** 숫자의 형태가 뚜렷하지 않고 심하게 흐릿한 경우
- **획의 단절:** 숫자를 구성하는 획이 중간에 끊겨 있는 경우
- **숫자 형태의 변형:** 일반적인 숫자 형태에서 크게 벗어나 모양이 변형된 경우

이러한 사례를 통해 이미지의 시각적 특징이 불분명하거나 일반적인 숫자 형태와 차이가 큰 경우 분류에 어려움을 겪을 수 있음을 확인했습니다.

## 시행착오 및 개선 과정

### 1. 역전파 과정에서의 연산 순서

역전파를 구현하는 과정에서 출력층의 오차 항(`output delta`)을 계산하기 전에 가중치를 먼저 업데이트하는 실수가 있었습니다.

역전파 과정에서 사용하는 오차 항은 해당 시점의 가중치를 기준으로 계산해야 하므로, 오차 항을 먼저 계산한 뒤 가중치를 업데이트하도록 연산 순서를 수정했습니다.

### 2. 가중치 업데이트를 위한 평균 연산 구현

미니배치 학습에서 여러 샘플의 기울기를 이용해 가중치를 업데이트하기 위해 평균 연산이 필요했습니다.

이를 위해 `mean` 함수를 별도로 구현했으며, 미니배치 단위로 계산한 기울기를 평균 내어 가중치와 편향을 업데이트하도록 구성했습니다.

### 3. 행렬 및 벡터의 형태 통일

구현 초기에는 입력 데이터를 열벡터로 사용할지에 대한 기준을 명확히 정하지 않아 행렬 연산 과정에서 형태를 맞추는 데 어려움이 있었습니다.

이를 통해 신경망을 구현하기 전에 입력 데이터, 가중치, 편향의 차원과 벡터 표현 방식을 미리 정의하는 것이 중요하다는 점을 배웠습니다.
