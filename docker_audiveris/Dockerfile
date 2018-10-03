FROM debian

RUN apt-get clean

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade

# install various libraries
RUN apt-get install -y wget git vim curl unzip zip

# install java-jdk-1.8(recommended)
RUN apt-get install -y openjdk-8-jdk

# install gradle 4.9 manually
# In case using apt-get, you cannot install latest gradle and it cannot build audiveris
# In case using sdkman, you cannnot 'RUN sdkman install' on Dockerfile
# You can install gradle in other way if you resoleve above problems.
WORKDIR /home
RUN wget https://services.gradle.org/distributions/gradle-4.9-bin.zip
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-4.9-bin.zip
ENV PATH $PATH:/opt/gradle/gradle-4.9/bin

# install tesseract-ocr
RUN apt-get install -y tesseract-ocr-dev tesseract-ocr tesseract-ocr-jpn

# git clone audiveris
# You git cline on deverpment branch where cli audiveris is available.
RUN git clone -b development --single-branch https://github.com/Audiveris/audiveris.git
WORKDIR /home/audiveris
RUN gradle clean build

WORKDIR /home/audiveris/build/distributions
RUN unzip Audiveris.zip
RUN bash Audiveris/bin/Audiveris -help

WORKDIR /home/audiveris
ENV PATH $PATH:/home/audiveris/build/distributions/Audiveris/bin

# RUN bash /home/audiveris/build/distributions/Audiveris/bin/Audiveris -batch -help
# Audiveris -batch -export Dichterliebe01.pdf -output test
# Audiveris -batch -print Dichterliebe01.pdf -output test