### django 설치
- python -m pip install Django

### nginx 설치
- apt install nginx
- ufw allow 'Nginx Full' //ip rule 설정
- /etc/nginx/sites-available/default 파일을 configuration
- 특히 파일 디렉토리 접근 시 404에러 나는 것을 막기 위해 try_files $uri $uri/ =404;를 반드시 주석처리

### 아나콘다 설치
- wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
- yes/no 물으면 다 yes
- 가상환경 생성할 때, python version은 3.6으로 할것. tensorflow에서 아직 3.8을 지원 안함

### 텐서플로우, 케라스 설치
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install tensorflow
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install keras

### uwsgi 설치
- conda config --add channels conda-forge
- conda install uwsgi

### uwsgi 데몬으로 만들기
- django의 manage.py가 있는 폴더에 uwsgi.ini 파일 생성

### uwsgi 서비스 등록/부팅시 자동실행 시키기
- /lib/systemd/system/dx.service 파일 생성
- sudo systemctl enable dx.service

### uwsgi 서비스 제거
- sudo systemctl disable dx.service

### uwsgi 서비스 상태조회/중지/재시작
- sudo systemctl status dx.service 또는 service dx status
- sudo systemctl stop dx.service 또는 service dx stop
- sudo systemctl restart dx.service 또는 service dx restart

### redis 바이너리 설치
- apt install redis-server
- 자동으로 서비스 등록됨

### redis 소스 설치
- wget http://download.redis.io/redis-stable.tar.gz
- tar xvzf redis-stable.tar.gz
- cd redis-stable
- make

### redis 실행(소스로 설치한 경우)
- redis-server

### redis 동작 확인
- redis-cli ping
- PONG 응답이 와야 함

### 윈도우에서 redis 설치
- https://github.com/MicrosoftArchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.msi 설치
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install redis

### celery 설치
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install celery

### 윈도우에서 celery 설치(4.4 버전 + gevent)
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install celery==4.4
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install gevent

### openpyxl 설치
- pip --trusted-host pypi.org --trusted-host files.pythonhosted.org install openpyxl

### pillow 설치(openpyxl에서 이미지 컨트롤할 때 사용)
- pip install Pillow

### beautiful soup 설치
- pip install beautifulsoup4

### requests 설치
- pip install requests

### django app 생성
- python manage.py startapp app이름

### pytorch + cuda toolkit설치
- conda install pytorch cudatoolkit=10.2 -c pytorch

### pytorch-transformers 설치
- pip pytorch-transformers

### keras ktrain 설치
- pip install ktrain
- tensorflow 2.1버전부터는 tensorflow-gpu를 따로 설치하지 않아도 됨(포함되어 있음)
- tensorflow 2.1버전은 cuda 10.1 + cudnn 10.1 까지 지원
- 하나의 Machine에 여러버전의 cuda를 깔 수 있다.
- cudnn은 nvidia 사이트에 회원가입해야 다운로드 받을 수 있으며, 설치가 아닌 다운로드 형태의 바이너리다.
- cudnn 및 cuda를 사용하려면 PATH 설정을 해줘야 한다.

### google bert 코드를 사용하려면 gin, tensorflow-hub 패키지를 설치해야 한다.
- pip install gin-config
- pip install tensorflow-hub
