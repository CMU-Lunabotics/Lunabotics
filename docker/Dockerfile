### SET UP BASE IMAGE ### 
# ROS distribution to use
ARG ROS_DISTRO=humble

########################################
# Base Image for ARM 64 architecture #
########################################
FROM arm64v8/ros:${ROS_DISTRO} AS base
ENV ROS_DISTRO=${ROS_DISTRO}
SHELL ["/bin/bash", "-c"]

# Install basic apt packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    git libcanberra-gtk-module libcanberra-gtk3-module fuse3 libfuse2 libqt5svg5-dev \
    python3-pip python3-opencv python3-pyqt5.qtwebengine

# Create a workspace
RUN mkdir -p /lunabotics/src
WORKDIR /lunabotics

#####################
# Development Image #
#####################
FROM base AS dev
ENV DISPLAY=:0

# Dev container arguments
ARG USERNAME=devuser
ARG UID=1000
ARG GID=${UID}

# install develoment tools 
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-${ROS_DISTRO}-ros-gz ros-$ROS_DISTRO-rviz2

# Install VNC and window manager
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-${ROS_DISTRO}-ros-gz \
    ros-$ROS_DISTRO-rviz2 \
    tigervnc-standalone-server \
    tigervnc-common \
    xfce4 \
    xfce4-goodies \
    dbus-x11 \
    mesa-utils \
    libgl1-mesa-dri

# Create new user and home directory
RUN groupadd --gid $GID $USERNAME \
    && useradd --uid ${GID} --gid ${UID} --create-home ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && mkdir -p /home/${USERNAME} \
    && chown -R ${UID}:${GID} /home/${USERNAME}

# Set the ownership of the overlay workspace to the new user
RUN chown -R ${UID}:${GID} /lunabotics

# Expose VNC port
EXPOSE 5901

### SET UP DEVELOPMENT IMAGE ### 