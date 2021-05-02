---
layout: post
title: "Deep Learning Development Environment"
---
## GPGPU
- General-Purpose computing on Graphics Processing Units
- 컴퓨터 그래픽스 계산이 아닌, CPU가 맡았던 응용 프로그램들의 계산에 GPU를 사용하는 기술

## CUDA
- Compute Unified Device Architecture
- NVIDIA에서 제공하는 GPGPU 도구
- 지포스8 이상의 그래픽카드에서만 지원
- C, Python, Java 등으로 작성된 인터페이스 지원

## 딥러닝에서 CUDA 사용
- 사용할 딥러닝 라이브러리가 지원하는 CUDA 버전을 확인한 후, 설치된 그래픽카드 드라이버가 해당 CUDA 버전을 지원하는지 확인
	- 딥러닝 라이브러리(Tensorflow, Pytorch, ...)가 지원하는 CUDA 버전
		- [Tensorflow Windows CUDA 지원](https://www.tensorflow.org/install/source_windows#tested_build_configurations)
		- [Tensorflow Linux/macOS CUDA 지원](https://www.tensorflow.org/install/source#tested_build_configurations)
		- [Pytorch CUDA 지원](https://pytorch.org/get-started/locally/)
	- 그래픽카드 드라이버가 지원하는 CUDA 버전
		- [그래픽카드 드라이버 CUDA 지원](https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility)
- 최신 그래픽카드 드라이버 설치
	- [그래픽카드 드라이버 다운로드](https://www.nvidia.com/download/index.aspx?lang=en-us#)
	- 다운로드 타입에 GRD와 SD가 있는데, SD선택하면 됨 [(참고)](https://www.reddit.com/r/nvidia/comments/d3dg88/game_ready_driver_vs_studio_driver_for_deep/)
- CUDA Toolkit 설치
  - CUDA Toolkit을 설치해야 딥러닝 라이브러리에서 CUDA를 사용할 수 있음
	- 원하는 버전에 맞는 CUDA Toolkit을 설치
	- 하나의 머신에 여러 버전 설치 가능, PATH 설정으로 선택
	- [버전별 CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive)
- 확인
```bash
nvidia-smi
```

## 참조
- <https://ko.wikipedia.org/wiki/GPGPU>
