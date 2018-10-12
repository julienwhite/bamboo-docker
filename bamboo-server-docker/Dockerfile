#############################################################
# BAMBOO SERVER - DOCKER INSTALL SCRIPT
#------------------------------------------------------------
# NAMING CONVENTION:
# B - Bamboo | S - Server | J - Java
#------------------------------------------------------------
# INSTRUCTIONS:
# Place Dockerfile in a folder. cd to folder. build image. run image
# open URL: IP:PORT and go through installation process
#------------------------------------------------------------
# DOCKER COMMANDS:
# Build: docker build . -t bs --no-cache
# Run (as local docker container): docker run -d -p YOURIP:8090:8085 bs
#############################################################
FROM centos:7
#---- Environment variables ----
# Java 
ENV JH=/usr/java
ENV JAVA_HOME=${JH}/jre1.8.0_161
# Bamboo
ENV BH=/home/bamboo-home
ENV BI=/home/bamboo-install
ENV BV=atlassian-bamboo-6.6.3
ENV BIP=${BI}/${BV}/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties
ENV BS_START=${BI}/${BV}/bin/start-bamboo.sh
#---- Commands ----
USER root
# create Java Home and Bamboo Server folder
RUN mkdir ${BI}; \
mkdir ${BH}; \
mkdir ${JH}; \
# Install wget net-tools;
yum install -y wget net-tools; \
# download and install JRE 8
cd ${JH}; \
wget -O jre-8u161-linux-x64.tar.gz http://javadl.oracle.com/webapps/download/AutoDL?BundleId=230532_2f38c3b165be4555a1fa6e98c45e0808; \
tar -xvf jre-8u161-linux-x64.tar.gz; \
rm -rf jre-8u161-linux-x64.tar.gz; \
# download and install bamboo server
cd ${BI}; \
wget https://www.atlassian.com/software/bamboo/downloads/binary/${BV}.tar.gz; \
tar -xvf ${BV}.tar.gz; \
RL=`grep -n bamboo.home= ${BIP} | head -n1 | cut -d: -f1`; \
sed -i "${RL}i bamboo.home=${BH}" ${BIP}; \
cat ${BIP} && rm -rf ${BI}/${BV}.tar.gz
EXPOSE 8085
CMD ["sh", "-c", "sh $BS_START -fg"]
