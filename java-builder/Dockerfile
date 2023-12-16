FROM openjdk:8u342 AS builder

# 手动安装 jdk
# RUN  mkdir /opt/java
# RUN yum update -y && yum install wget git vim -y
# RUN wget -P /tmp --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
#     http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz && \
#     tar -zxvf /tmp/jdk-8u131-linux-x64.tar.gz -C /opt/java

# ENV JAVA_HOME=/opt/java/jdk1.8.0_131 \
#     JRE_HOME=${JAVA_HOME}/jre \
#     CLASSPATH=.${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH \
#     JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin \
#     MAVEN_HOME=/opt/java/apache-maven-3.8.6 \
#     PATH=$PATH:$MAVEN_HOME/bin

# 手动安装 maven
RUN apt update -y && apt install wget -y
RUN wget -P /tmp https://dlcdn.apache.org/maven/maven-3/3.9.2/binaries/apache-maven-3.9.2-bin.tar.gz && \
    tar -xvf /tmp/apache-maven-3.9.2-bin.tar.gz -C /usr/local && \
    ln -s /usr/local/apache-maven-3.9.2/bin/mvn /usr/bin/mvn

WORKDIR /app
COPY . .

# COPY ./settings.xml /usr/local/apache-maven-3.9.2/conf/settings.xml
RUN mvn install:install-file -DgroupId=com.aspose -DartifactId=aspose-words -Dversion=20.3 -Dpackaging=jar -Dfile=aspose-words-20.3.jar  && \
    mvn clean package

FROM openjdk:8u342

WORKDIR /app
RUN mkdir logs
COPY --from=builder /app/*.jar /app/
COPY ./run.sh .
RUN chmod 777  /app/run.sh
# 执行命令
ENTRYPOINT ["/app/run.sh","start"]
