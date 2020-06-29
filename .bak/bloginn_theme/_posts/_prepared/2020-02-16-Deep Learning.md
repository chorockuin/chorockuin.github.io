---
layout: post
title: "Deep Learning"
date: 2020-02-16
<!--banner_image: .jpg-->
tags: [AI, Development]
---
* ML(Machine Learning)
	+ 지도 학습(Supervised Learning)
	+ 강화 학습(Reinforcement Learning)
	+ 비지도 학습(Unsupervised Learning)

* DL(Deep Learning)

* GPGPU(General-Purpose computing on Graphics Processing Units)
	+ GPU 상의 범용(그래픽스 전용이 아닌) 계산

* CUDA(Computed Unified Device Architecture)
	+ NVIDIA에서 제공하는 GPGPU 도구
	+ 지포스8 이상에서만 지원
	+ C, 파이선, 자바등으로 작성된 인터페이스 지원
	+ 그래픽카드 정보 확인
		- lshw -C display
		- lspci | grep -i VGA
		- nvidia-smi --query | fgrep 'Product Name'
	+ GPU 사용 상태 확인
		- watch -d -n 0.5 nvidia-smi
	+ 드라이버가 필요한 모든 장치 표시
		- ubuntu-drivers devices
	+ NVIDIA 드라이버 확인
		- cat /proc/driver/nvidia/version
	+ CPU 코어 수 확인
		- cat /proc/cpuinfo | grep processor | wc -l
	+ CUDA Toolkit 설치
		- https://developer.nvidia.com/cuda-10.1-download-archive-update2?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal
	+ CUDA Compiler 버전 확인
		- nvcc -V
	+ Tensorflow GPU 지원
		- https://www.tensorflow.org/install/gpu

* MKL(Math Kernel Library)
	+ 과학, 공학, 금융 응용 프로그램에 최적화된 수학 라이브러리

* DNN(Deep Neural Network)
	+ 은닉층이 많은 NN

* MXNet
	+ DL 라이브러리(http://beta.mxnet.io/)
	+ pip install mxnet-cu92mkl

* GluonNLP
	+ NLP DL 라이브러리(https://gluon-nlp.mxnet.io/)
	+ Word Embedding, Language Modeling, Machine Translation, Text Classification, Sentiment Analysis, Parsing(의존성 구문 분석), Natrual Language Inference(자연어 추론), Text Generation
	+ MXNet 이용, BERT 라이브러리 제공
	+ pip install gluonnlp
