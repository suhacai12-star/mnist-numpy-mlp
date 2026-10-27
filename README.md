# mnist-numpy-mlp
MNIST 손글씨 데이터셋을 활용해 NumPy로 신경망을 직접 구현하고, 학습 결과와 오분류 이미지를 분석하는 프로젝트
## Dataset

This project uses the MNIST handwritten digit dataset, loaded through `tensorflow.keras.datasets`.

- **Dataset:** MNIST handwritten digit dataset
- **Source:** [Keras MNIST Dataset Documentation](https://keras.io/api/datasets/mnist/)
- **Description:** 60,000 training images and 10,000 test images of handwritten digits (0–9).

The dataset is loaded using TensorFlow/Keras. The neural network architecture, forward propagation, backpropagation, and training process are implemented using NumPy.

The dataset itself is not included in this repository; it is downloaded through the dataset-loading function when needed.
