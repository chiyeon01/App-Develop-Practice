# Ubuntu 베이스 이미지 사용
FROM ubuntu:20.04

# 기본 패키지 설치 및 업데이트
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    xz-utils \
    zip \
    libglu1-mesa

# Flutter 설치
RUN curl -LO https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.3.10-stable.tar.xz && \
    tar xf flutter_linux_3.3.10-stable.tar.xz && \
    mv flutter /usr/local/flutter

# 환경 변수 설정
ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Flutter 의존성 설치
RUN flutter doctor

# 필요한 경우 추가 패키지 설치
# RUN apt-get install -y 추가 패키지

# Flutter 프리컴파일을 위한 실행
RUN flutter precache

# 디버깅을 위한 포트 노출
EXPOSE 9222
