FROM jadehh/miniconda3:python-3.6.9
## pip环境设置
RUN rm -r /root/miniconda3/bin/pip
RUN ln -s /root/miniconda3/envs/python3.6.9/bin/pip /root/miniconda3/bin/pip
RUN pip install tornado==4.5.1
RUN pip install scipy==1.5.4
RUN pip install imutils==0.5.4
RUN pip install spyne==2.13.16
RUN pip install lxml==4.7.1
RUN pip install requests==2.27.1
RUN pip install suds==1.1.2
RUN pip install pyclipper==1.3.0
RUN pip install shapely==1.8.0
RUN pip install https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/JadeV1.8.1/jade-1.8.1-py3-none-any.whl
RUN pip install https://gh.con.sh/https://github.com/jadehh/pythonTools/releases/download/OpencvToolsV1.2.4/opencv_tools-1.2.4-py3-none-any.whl
RUN pip install https://gh.ddlc.top/https://github.com/jadehh/paddle/releases/download/v2.1.0-gpu-linux-py3.6/paddle_gpu_clean-2.1.0-cp36-cp36m-manylinux1_x86_64.whl




