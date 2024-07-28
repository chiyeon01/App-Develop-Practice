FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    xz-utils \
    zip \
    libglu1-mesa \
    ninja-build \
    build-essential \
    cmake

# Install Flutter
RUN curl -LO https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.3.10-stable.tar.xz && \
    tar xf flutter_linux_3.3.10-stable.tar.xz && \
    mv flutter /usr/local/flutter

# Install Android SDK
RUN mkdir -p /usr/local/android-sdk-linux && \
    cd /usr/local/android-sdk-linux && \
    curl -O https://dl.google.com/android/repository/commandlinetools-linux-7583922_latest.zip && \
    unzip commandlinetools-linux-7583922_latest.zip && \
    rm commandlinetools-linux-7583922_latest.zip && \
    mkdir -p cmdline-tools/latest && \
    mv cmdline-tools/* cmdline-tools/latest

# Set environment variables
ENV ANDROID_HOME=/usr/local/android-sdk-linux
ENV PATH=$PATH:/usr/local/flutter/bin:/usr/local/android-sdk-linux/cmdline-tools/latest/bin:/usr/local/android-sdk-linux/platform-tools:/usr/local/android-sdk-linux/emulator

# Accept Android SDK licenses
RUN yes | sdkmanager --licenses

# Install required SDK packages
RUN sdkmanager "platform-tools" "platforms;android-30" "build-tools;30.0.3"

# Run flutter doctor to install dependencies
RUN flutter doctor --android-licenses
RUN flutter doctor
RUN flutter precache
