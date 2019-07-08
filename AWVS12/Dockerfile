FROM ubuntu:latest

RUN mkdir /data
WORKDIR /data
RUN apt-get update && apt-get upgrade -y && apt-get install -y sudo apt-utils net-tools && rm -rf /var/lib/apt/lists/*
RUN apt-get update && sudo apt-get install libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 libx11-xcb1 -y
COPY ./acunetix_trial.sh .
RUN chmod u+x acunetix_trial.sh
#自行修改邮箱、密码
RUN sh -c '/bin/echo -e "\nyes\nubuntu\nadmin@test.com\nAa123456\nAa123456\n"| ./acunetix_trial.sh'
#wvs版本发生变化的话，请修改下方的版本号。版本号在 acunetix_trail.sh 中有
WORKDIR /home/acunetix/.acunetix_trial/v_190515149/scanner
COPY ./patch_awvs .
USER root
RUN chmod u+x ./patch_awvs
CMD chmod u+x /home/acunetix/.acunetix_trial/start.sh
USER acunetix
CMD /home/acunetix/.acunetix_trial/start.sh