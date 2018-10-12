#############################################################
# BAMBOO REMOTE AGENT - DOCKER INSTALL SCRIPT
#------------------------------------------------------------
# B - Bamboo | A - Agent | S - Server | J - Java
#------------------------------------------------------------
# REQUIREMENT: Bamboo Server Installed and running.
#------------------------------------------------------------
# INSTRUCTIONS:
# 1. Place Dockerfile in a folder.
# 2. update BS_IP variable with your Bamboo server IP:PORT 
# 3. DL Remote Agent Jar from http://${BS_IP}/admin/agent/addRemoteAgent.action to folder root
# 4. update BA_IMG variable with downloaded filename
# 5. cd to folder root. Build. Run.
# 6. Go to your bamboo server > Agent and approve connection request
#------------------------------------------------------------
# DOCKER COMMANDS:
# Build: docker build . -t ba --no-cache
# Run: docker run -d ba
#############################################################
FROM centos:7
#---- Environment variables ----
# Network config
ENV BS_IP=10.240.20.84:8090
ENV BS_URL=http://${BS_IP}/agentServer/
# Paths config
ENV JH=/usr/java
ENV BH=/home/bamboo-agent
ENV JAVA_HOME=/usr/java/jre1.8.0_161/bin
# Images
ENV J_IMG=jre-8u161-linux-x64.tar.gz
ENV J_URL=http://javadl.oracle.com/webapps/download/AutoDL?BundleId=230532_2f38c3b165be4555a1fa6e98c45e0808
ENV BA_IMG=atlassian-bamboo-agent-installer-6.4.0.jar
#---- Commands ----
USER root
# create Java Home and Bamboo Agent folder
RUN mkdir $JH; \
mkdir $BH; \
# Install wget net-tools;
yum install -y wget net-tools;
# copy BA image to BA folder
COPY ${BA_IMG} ${BH}/${BA_IMG}
# pull JRE image to JH folder and extract it
RUN cd $JH; \
wget -O ${J_IMG} ${J_URL}; \
tar -xvf ${J_IMG}; \
rm -rf ${J_IMG}; \
ls -ltrh;
RUN cd $BH; \
echo $PATH;
# export Java path and run BA to BS connection
CMD ["sh", "-c", "export PATH=$JAVA_HOME:$PATH && java -jar $BH/$BA_IMG $BS_URL"]
# java -jar atlassian-bamboo-agent-installer-6.6.3.jar http://192.168.43.154:8090/agentServer/