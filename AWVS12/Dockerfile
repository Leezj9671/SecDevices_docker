FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive

USER root
WORKDIR /data
COPY ./acunetix_trial.sh .
RUN sed -i "s@http://.*archive.ubuntu.com@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
  && sed -i "s@http://.*security.ubuntu.com@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y sudo apt-utils net-tools systemd \ 
  && apt-get install libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 libx11-xcb1 sudo systemd apt-utils net-tools -y \
  && chmod u+x acunetix_trial.sh 
#自行修改邮箱、密码
RUN sh -c '/bin/echo -e "\nyes\nubuntu\nadmin@test.com\nAa123456\nAa123456\n"| ./acunetix_trial.sh' \
  && chmod u+x /home/acunetix/.acunetix_trial/start.sh

#wvs版本发生变化的话，请修改下方的版本号。版本号在 acunetix_trail.sh 中有
WORKDIR /home/acunetix/.acunetix_trial/v_190515149/scanner 
COPY patch_awvs .
RUN chmod u+x patch_awvs

USER acunetix
CMD /home/acunetix/.acunetix_trial/start.sh
