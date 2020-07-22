FROM ringcentral/chrome-vnc:chrome75

ENV DISPLAY :99

# Install git, wget, Open JDK8  
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - && \
    apt-get update -yq && \
    apt-get install -y git wget openjdk-8-jdk 

# Install maven
RUN wget --no-verbose -O /tmp/apache-maven-3.5.4-bin.tar.gz http://www-us.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz && \
    tar xzf /tmp/apache-maven-3.5.4-bin.tar.gz -C /opt/ && \
    ln -s /opt/apache-maven-3.5.4 /opt/maven && \
    ln -s /opt/maven/bin/mvn /usr/local/bin  && \
    rm -f /tmp/apache-maven-3.5.4-bin.tar.gz

ENV MAVEN_HOME /opt/maven

RUN apt-get update && apt-get -qqy --no-install-recommends install python2.7
RUN ln -s /usr/bin/python2.7 /bin/python
RUN wget https://bootstrap.pypa.io/get-pip.py && python2.7 get-pip.py && rm get-pip.py
RUN pip install compago

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64
RUN chmod +x /usr/local/bin/dumb-init

ENV TZ 'Asia/Shanghai'
RUN echo $TZ > /etc/timezone && \
    apt-get update && apt-get install -y tzdata && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean
