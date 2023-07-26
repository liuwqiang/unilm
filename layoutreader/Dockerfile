FROM docker.wanfangdata.com.cn/wfk8s/pytorch:1.12.0-cuda11.3-cudnn8-devel
ARG http_proxy
ARG https_proxy

ENV TZ=Asia/Shanghai \
DEBIAN_FRONTEND=noninteractive \
http_proxy=$http_proxy \
https_proxy=$http_proxy

RUN apt-get update && apt-get install -y git && python -m pip install packaging
WORKDIR build
RUN git clone https://github.com/NVIDIA/apex.git && git clone https://github.com/microsoft/unilm.git
RUN cd apex && pip install -v --disable-pip-version-check --no-cache-dir --no-build-isolation --global-option="--cpp_ext" --global-option="--cuda_ext" ./
RUN cd unilm/layoutreader && pip install .
RUN pip install nltk && python -c "import nltk; nltk.download('punkt')"
WORKDIR /layoutreader
ENV http_proxy=
ENV https_proxy=

CMD ["python"]
