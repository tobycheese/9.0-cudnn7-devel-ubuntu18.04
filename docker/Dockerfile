### Dockerfile with Ubuntu 18.04 and cuda 9.0
### Changes are indicated by CHANGED
### Everything else was copied together from the original Dockerfiles (as per comments)

### 1st part from https://gitlab.com/nvidia/cuda/blob/ubuntu18.04/10.0/base/Dockerfile

FROM ubuntu:18.04
# CHANGED
#LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"
LABEL maintainer="tobycheese https://github.com/tobycheese/"

# CHANGED: below, add the two repos from 17.04 and 16.04 so all packages are found
RUN apt-get update && apt-get install -y --no-install-recommends gnupg2 curl ca-certificates && \
    curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub | apt-key add - && \
    echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/cuda.list && \
    echo "deb https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list && \
    echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1704/x86_64 /" >> /etc/apt/sources.list.d/cuda.list && \
    echo "deb https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" >> /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get purge --autoremove -y curl && \
    rm -rf /var/lib/apt/lists/*

### end 1st part from from https://gitlab.com/nvidia/cuda/blob/ubuntu18.04/10.0/base/Dockerfile

### 2nd part from https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/base/Dockerfile

ENV CUDA_VERSION 9.0.176

ENV CUDA_PKG_VERSION 9-0=$CUDA_VERSION-1
RUN apt-get update && apt-get install -y --no-install-recommends \
        cuda-cudart-$CUDA_PKG_VERSION && \
    ln -s cuda-9.0 /usr/local/cuda && \
    rm -rf /var/lib/apt/lists/*

# CHANGED: commented out
# nvidia-docker 1.0
#LABEL com.nvidia.volumes.needed="nvidia_driver"
#LABEL com.nvidia.cuda.version="${CUDA_VERSION}"

RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=9.0"

### end 2nd part from https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/base/Dockerfile

### all of https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/runtime/Dockerfile

ENV NCCL_VERSION 2.3.7

RUN apt-get update && apt-get install -y --no-install-recommends \
        cuda-libraries-$CUDA_PKG_VERSION \
        cuda-cublas-9-0=9.0.176.4-1 \
        libnccl2=$NCCL_VERSION-1+cuda9.0 && \
    apt-mark hold libnccl2 && \
    rm -rf /var/lib/apt/lists/*

### end all of from https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/runtime/Dockerfile

### all of https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/devel/Dockerfile

RUN apt-get update && apt-get install -y --no-install-recommends \
        cuda-libraries-dev-$CUDA_PKG_VERSION \
        cuda-nvml-dev-$CUDA_PKG_VERSION \
        cuda-minimal-build-$CUDA_PKG_VERSION \
        cuda-command-line-tools-$CUDA_PKG_VERSION \
        cuda-core-9-0=9.0.176.3-1 \
        cuda-cublas-dev-9-0=9.0.176.4-1 \
        libnccl-dev=$NCCL_VERSION-1+cuda9.0 && \
    rm -rf /var/lib/apt/lists/*

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs

### end all of https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/devel/Dockerfile

### all of https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/devel/cudnn7/Dockerfile

ENV CUDNN_VERSION 7.4.1.5
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

RUN apt-get update && apt-get install -y --no-install-recommends \
            libcudnn7=$CUDNN_VERSION-1+cuda9.0 \
            libcudnn7-dev=$CUDNN_VERSION-1+cuda9.0 && \
    apt-mark hold libcudnn7 && \
    rm -rf /var/lib/apt/lists/*

### end all of https://gitlab.com/nvidia/cuda/blob/ubuntu16.04/9.0/devel/cudnn7/Dockerfile