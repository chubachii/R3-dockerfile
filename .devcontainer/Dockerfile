FROM ubuntu:18.04

# 環境変数
#ENV http_proxy 'http://id:pass@proxy:port'
#ENV https_proxy 'https://id:pass@proxy:port' 

# apt のプロキシ設定
#RUN echo "Acquire::http::proxy \"id:pass@proxy:port/\";" >> /etc/apt/apt.conf && \
    #echo "Acquire::https::proxy \"id:pass@proxy:port/\";" >> /etc/apt/apt.conf

# apt のアップデート
RUN apt-get update && apt-get upgrade -y 

# 依存関係のインストール
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y  make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    libgtk2.0-dev libavcodec-dev libavformat-dev libswscale-dev v4l-utils libv4l-dev libcanberra-gtk* \
    xz-utils tk-dev libffi-dev git gcc cmake unzip sudo python3-dev python3-pip python3-setuptools  \
    jupyter jupyter-qtconsole spyder3 python3-ptyprocess python3-terminado python3-tornado

# pip のプロキシ設定
#RUN set HTTP_PROXY = http://id:pass@proxy:port && \
    #set HTTPS_PROXY = http://id:pass@proxy:port

# pip のアップデート
RUN pip3 install -U jupyterlab nteract_on_jupyter && \
    pip3 install pip==20.1.1 

# ライブラリインストール
# OpenCV 
RUN apt-get install -y libopencv-dev libopencv-core-dev libopencv-contrib-dev opencv-data \
    python3-opencv=3.2.0+dfsg-4ubuntu0.1

# Mediapipe 
RUN pip3 install absl-py protobuf && \
    pip3 install --no-deps mediapipe==0.8.3

# TensorFlow
RUN pip3 install tensorflow==2.1.0 --ignore-installed --user

# Pyaudio
RUN apt-get install -y python3-pyaudio

# Others
RUN pip3 install numpy==1.19.3 matplotlib Scipy

# 日本語設定 
RUN apt-get install -y language-pack-ja-base language-pack-ja locales && \
    locale-gen ja_JP.UTF-8 && \
    echo "export LANG='ja_JP.UTF-8'" >> "${HOME}/.profile" && \
    echo "export LANG='ja_JP.UTF-8'" >> "${HOME}/.bashrc"