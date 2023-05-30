FROM nginx:1.19

# install apt-utils
RUN apt-get update 

RUN apt-get install apt-utils -y

RUN apt-get install nmap -y

RUN apt-get install bash -y

# replace sh with bash
RUN rm /bin/sh && ln -s /bin/bash /bin/sh