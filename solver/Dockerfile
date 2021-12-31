FROM ubuntu:20.04

#------------------------------------------------
# (1) install fundamental commands
#------------------------------------------------
RUN \
    apt update && \
    apt -y upgrade && \
    apt install -y curl git man unzip vim wget sudo

#   Hint: you may want to additionally install the followings. 
#   apt install -y build-essential
#   apt install -y software-properties-common

#------------------------------------------------
# (2) clone the 2022solver directory to /
#------------------------------------------------
RUN git clone https://github.com/core-challenge/2022solver.git



