FROM ubuntu:22.04
RUN apt update -y && \
    apt install openjdk-21-jdk maven git -y
WORKDIR /app
RUN git clone https://github.com/Siva825/spring-petclinic.git .
RUN mvn clean package -DskipTests
EXPOSE 8080
CMD ["java", "-jar", "/app/target/spring-petclinic-3.5.0-SNAPSHOT.jar"]
