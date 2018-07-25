FROM dockerhub.ygomi.com/ubuntu:14.04
USER root

COPY 	./startup.sh /

RUN	sudo rm -rf /etc/apt/sources.list &&\
        . /etc/lsb-release &&\
        echo deb http://mirrors.ygomi.com/pub/ubuntu ${DISTRIB_CODENAME} main restricted universe multiverse |tee -a /etc/apt/sources.list &&\
        echo deb http://mirrors.ygomi.com/pub/ubuntu ${DISTRIB_CODENAME}-updates main restricted universe multiverse |tee -a /etc/apt/sources.list &&\
        echo deb http://mirrors.ygomi.com/pub/ubuntu ${DISTRIB_CODENAME}-backports main restricted universe multiverse |tee -a /etc/apt/sources.list &&\
        echo deb http://mirrors.ygomi.com/pub/ubuntu ${DISTRIB_CODENAME}-security main restricted universe multiverse |tee -a /etc/apt/sources.list &&\	
    apt-get update && apt-get install -y --no-install-recommends --force-yes \
	software-properties-common \
	wget=1.15-1ubuntu1 \
	ssh


RUN 	sed -i "s/without-password/yes/g" /etc/ssh/sshd_config &&\
	#ygomi dns
	echo 10.69.6.110	pub-repo.roaddb.ygomi.com |tee -a /etc/hosts &&\
	echo 112.124.140.210	cn.archive.ubuntu.com|tee -a /etc/hosts &&\
	echo 10.69.6.110	mirrors.ygomi.com|tee -a /etc/hosts &&\
	#create roaddb user
 	useradd -d /home/roaddb -m roaddb &&\
 	echo "roaddb ALL = (root) NOPASSWD:ALL"| sudo tee /etc/sudoers.d/roaddb &&\
	chmod 0440 /etc/sudoers.d/roaddb &&\
 	echo roaddb:test1234 | chpasswd &&\
 	mkdir /home/roaddb/.ssh &&\
 	touch /home/roaddb/.ssh/authorized_keys &&\
        wget -O /tmp/ssl.tar.gz2 http://repo.roaddb.ygomi.com/download/docker/ssl.tar.gz2 &&\
        sudo tar jvxf /tmp/ssl.tar.gz2 -C /home/roaddb/ &&\
        rm -rf /tmp/* &&\
 	chmod 0755 /startup.sh

##CMD	["bash"]

EXPOSE 22

ENTRYPOINT ["sh","/startup.sh"]

