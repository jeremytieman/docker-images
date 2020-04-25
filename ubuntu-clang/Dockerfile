FROM ubuntu:18.04

# Add git software repository
RUN apt-get update && apt-get install -y software-properties-common && \
  add-apt-repository -y ppa:git-core/ppa

# Make sure the image is updated, install some prerequisites,
# Download the latest version of Clang (official binary) for Ubuntu
# Extract the archive and add Clang to the PATH
RUN apt-get update && apt-get install -y \
  xz-utils \
  build-essential \
  curl \
  unzip \
  git \
  && rm -rf /var/lib/apt/lists/* \
  && curl -SL https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz \
  | tar -xJC . && \
  mv clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04 clang_10.0.0 && \
  echo 'export PATH=/clang_10.0.0/bin:$PATH' >> ~/.bashrc && \
  echo 'export LD_LIBRARY_PATH=/clang_10.0.0/lib:$LD_LIBRARY_PATH' >> ~/.bashrc && \
  echo 'export CC=/clang_10.0.0/bin/clang' >> ~/.bashrc && \
  echo 'export CXX=/clang_10.0.0/bin/clang++' >> ~/.bashrc

RUN curl -SL https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1-Linux-x86_64.sh --output /cmake-3.17.1-Linux-x86_64.sh && \
  chmod 775 /cmake-3.17.1-Linux-x86_64.sh && \
  /cmake-3.17.1-Linux-x86_64.sh --skip-license

RUN curl -SL https://github.com/ninja-build/ninja/releases/download/v1.10.0/ninja-linux.zip --output ninja-linux.zip && \
  unzip ninja-linux.zip -d /bin

# Start from a Bash prompt
CMD [ "/bin/bash" ]