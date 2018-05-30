# Copyright 2018 The TensorFlow Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# =============================================================================

ARG UBUNTU_VERSION="16.04"

FROM ubuntu:${UBUNTU_VERSION}

ARG TF_VERSION="1.8.0"
ARG PY_VERSION_SUFFIX=""

LABEL maintainer="TensorFlow Developers <developers@tensorflow.org>"

RUN apt-get update && apt-get install -y \
    python${PY_VERSION_SUFFIX} \
    python${PY_VERSION_SUFFIX}-pip
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip${PY_VERSION_SUFFIX} --no-cache-dir install tensorflow==${TF_VERSION}

# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]
