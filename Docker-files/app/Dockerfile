FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
# Increase Git buffer size
RUN git config --global http.postBuffer 104857600

# Shallow clone the repository
RUN git clone -b docker --depth 1 https://github.com/christian-pprogrammer/vprofile-project.git

RUN cd vprofile-project && git fetch && git checkout docker && mvn install


FROM tomcat:9.0-jre11 
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD [ "catalina.sh", "run" ]
WORKDIR /usr/local/tomcat/
VOLUME  /usr/local/tomcat/webapps
