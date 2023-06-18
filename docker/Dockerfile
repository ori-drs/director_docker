FROM ros:noetic-robot

ENV ROS_WS_DIR="/digiforest_ws"

WORKDIR ${ROS_WS_DIR}

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get -y install \
    git \
    python3-catkin-tools \
    python3-osrf-pycommon \
    python3-vcstool \
    apt-utils
 
# python-pcl
RUN apt-get install libpcl-dev python3-pip -y \
    && pip3 install Cython numpy==1.23.4 lxml

RUN mkdir -p ${ROS_WS_DIR}/src

WORKDIR ${ROS_WS_DIR}/src

RUN git clone https://github.com/ori-drs/python-pcl.git
    
WORKDIR ${ROS_WS_DIR}/src/python-pcl

RUN python3 setup.py build_ext --inplace \
    && python3 setup.py install
    
# cloning
WORKDIR ${ROS_WS_DIR}/src
RUN git clone https://github.com/ori-drs/PointCloudLibraryPlugin \
    && git clone https://github.com/ori-drs/director_digiforest.git \
    && git clone https://github.com/ori-drs/cv_utils.git \
    && git clone https://github.com/ori-drs/ctkPythonConsole.git \
    && git clone https://github.com/ori-drs/PythonQt.git \
    && git clone https://github.com/ori-drs/QtPropertyBrowser.git \
    && git clone https://github.com/ori-drs/digiforest_drs.git

# dependencies
RUN apt install -y ros-noetic-pcl-ros \ 
                     libqwt-qt5-dev \
                     qtscript5-dev \
                     qtbase5-private-dev \
                     qtmultimedia5-dev \
                     python3-pyqt5 \
    && pip install utm pymap3d
    
# building workspace
WORKDIR ${ROS_WS_DIR}
RUN source /opt/ros/noetic/setup.bash \
    && catkin init \
    && catkin config --extend /opt/ros/noetic \
    && catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release \
    && catkin build director_digiforest

ENV DEBIAN_FRONTEND=dialog

RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc \
 && echo "source ${ROS_WS_DIR}/devel/setup.bash" >> ~/.bashrc

