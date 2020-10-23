# 基础镜像
FROM ubuntu:16.04

# 将操作设为飞交互式
ENV DEBIAN_FRONTEND=noninteractive

# 安装常用软件
RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq wget curl git build-essential vim sudo lsb-release locales bash-completion

# 安装 ROS 桌面版（如果在国内环境可能需要换 ROS 源提高速度）
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN curl -sSL 'http://keyserver.ubuntu.com/pks/lookup?op=get&search=0xC1CF6E31E6BADE8868B172B4F42ED6FBAB17C654' | sudo apt-key add -
RUN apt-get update -q && \
    apt-get install -y ros-kinetic-desktop-full python-rosdep
RUN apt-get install -y ros-kinetic-perception-pcl
RUN apt-get install -y libgoogle-glog-dev
RUN rosdep init
RUN rosdep update

# G2O 相关
RUN apt-get install -y libqglviewer-dev
RUN apt-get install -y qtdeclarative5-dev
RUN apt-get install -y qt5-qmake
RUN apt-get install -y libsuitesparse-dev
RUN apt-get install -y libatlas-base-dev

# source ros setup 脚本
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc
RUN /bin/bash -c "source /root/.bashrc"

# 设置语言
RUN apt-get update
RUN apt-get install -y locales locales-all
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

# 设置工作目录
WORKDIR /root