# Devlop环境
FROM jadehh/miniconda3:amd64-4.9.2



## 1 Ascend-cann-toolkit安装
RUN wget https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/CANN/6.0.0.alpha001/Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run
RUN chmod +x Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run && \
    ./Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run --quiet --install && \
     rm Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run

ENV ASCEND_TOOLKIT_HOME=/usr/local/Ascend/ascend-toolkit/latest/
ENV PATH=$PATH:${ASCEND_TOOLKIT_HOME}/compiler/ccec_compiler/bin:${ASCEND_TOOLKIT_HOME}compiler/bin
ENV PYTHONPATH=$PYTHONPATH:${ASCEND_TOOLKIT_HOME}/compiler/python/site-packages:${ASCEND_TOOLKIT_HOME}/compiler/python/site-packages/auto_tune.egg/auto_tune:${ASCEND_TOOLKIT_HOME}/compiler/python/site-packages/schedule_search.egg:${ASCEND_TOOLKIT_HOME}/opp/op_impl/built-in/ai_core/tbe
ENV LD_LIBRARY_PATH=${ASCEND_TOOLKIT_HOME}/compiler/lib64:${ASCEND_TOOLKIT_HOME}/6.0.0.alpha001/add-ons:${ASCEND_TOOLKIT_HOME}/runtime/lib64:$LD_LIBRARY_PATH:${ASCEND_TOOLKIT_HOME}/x86_64-linux/devlib:${ASCEND_TOOLKIT_HOME}/aarch64-linux/devlib
ENV ASCEND_OPP_PATH=${ASCEND_TOOLKIT_HOME}/opp

## 安装pip环境
RUN pip install sympy==1.10.1
RUN pip install decorator==5.1.1
RUN pip install numpy==1.21.6