FROM maven:3-amazoncorretto-21

WORKDIR /app

COPY pom.xml .
RUN mvn exec:java || exit 0

COPY src src
RUN mvn compile

CMD ["mvn", "exec:java", "--offline"]
