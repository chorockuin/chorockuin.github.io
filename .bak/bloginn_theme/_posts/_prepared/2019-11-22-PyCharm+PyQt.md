---
layout: post
title: "PyCharm+PyQt"
date: 2019-11-22
<!--banner_image: .jpg-->
tags: [Coding, Development]
---
* 아나콘다 가상 환경 경로
	* 아나콘다 설치 위치\envs\가상 환경 이름

* 아나콘다 가상 환경 활성화
	* conda activate 가상 환경 이름

* 활성화된 가상 환경에 PyQt5 설치
	* pip install pyqt5
	* 아나콘다 설치 위치\envs\가상 환경 이름\Lib\site-packages\PyQt5 경로에 설치됨

* 활성화된 가상 환경에 PyQt5 유틸리티 설치
	* pip install pyqt5-tools
	* 아나콘다 설치 위치\envs\가상 환경 이름\Lib\site-packages\pyqt5_tools 경로에 설치됨
	* Qt Designer는 아나콘다 설치 위치\envs\가상 환경 이름\Lib\site-packages\pyqt5_tools\Qt\bin 경로에 설치됨

* PyCharm에 아나콘다 가상 환경 연결하기
	* File > Settings > Project > Project Interpreter > 설정 아이콘 > Add > Conda Environment > Existing environment

* Qt 디자이너에서 꾸민 UI(.ui 파일)를 파이썬 코드에 바인딩 하는 방법
	* uic 모듈을 이용하면 .ui 파일을 쉽게 로딩할 수 있다.
	* 나의 Form(Dialg, Window, ...)에 이벤트를 핸들링하는 함수를 추가했다면, uic 모듈에 self를 파라미터로 넘겨주어야 한다.

* Qt 디자이너에서 이벤트(Signal)을 핸들링(Slot)하는 방법
	* Edit > Edit Signals/Slots를 선택
	* 이벤트를 발생시키는 위젯(Button, List, ....)을 클릭, 드래그하면 이벤트를 핸들링할 위젯(Dialog, Window, ...)까지 선을 이을 수 있다.
	* 선을 잇고 난 후, 바로 뜨는 설정 창에서 핸들링할 이벤트(clicked(), released(), ...)를 선택하고, 실제로 핸들링할 함수의 이름을 정하고 OK를 누른다.
	* 핸들링할 함수를 위젯(Dialog, Windows, ...)에 정의, 동작을 구현한다.