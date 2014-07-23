from dockerfile/java
maintainer SequenceIQ

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
#RUN echo "deb http://downloads.sourceforge.net/project/sonar-pkg/deb binary/" >> /etc/apt/sources.list
RUN apt-get update && apt-get upgrade -y

RUN wget http://dist.sonar.codehaus.org/sonarqube-4.1.2.zip && unzip sonarqube-4.1.2.zip && mv sonarqube-4.1.2 /opt/sonar
RUN wget https://github.com/drewcrawford/sonarqube-docker-public-fork/raw/master/sonar-objective-c-plugin-dca-0.4.jar && mv sonar-objective-c-plugin-dca-0.4.jar /opt/sonar/extensions/plugins/sonar-objective-c-plugin-dca-0.4.jar

RUN sed -i 's|#wrapper.java.additional.7=-server|wrapper.java.additional.7=-server|g' /opt/sonar/conf/wrapper.conf

RUN sed -i 's|sonar.jdbc.password=sonar|sonar.jdbc.password=123qwe|g' /opt/sonar/conf/sonar.properties
RUN sed -i 's|sonar.jdbc.url=jdbc:h2|#sonar.jdbc.url=jdbc:h2|g' /opt/sonar/conf/sonar.properties
RUN sed -i 's|#sonar.jdbc.url=jdbc:mysql://localhost|sonar.jdbc.url=jdbc:mysql://${env:DB_PORT_3306_TCP_ADDR}|g' /opt/sonar/conf/sonar.properties

CMD ["/opt/sonar/bin/linux-x86-64/sonar.sh", "console", "/bin/bash"]