FROM eclipse-temurin:21-jdk AS builder

WORKDIR /usr/src/app

COPY gradlew* settings.gradle* build.gradle .
COPY ./gradle ./gradle

RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepos

COPY . .
COPY ./pb ./proto
RUN chmod +x ./gradlew
RUN ./gradlew installDist -PprotoSourceDir=./proto

FROM eclipse-temurin:21-jre AS finale

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/build/install/opentelemetry-demo-ad ./opentelemetry-demo-ad

ENV AD_PORT=9099

ENTRYPOINT ["./opentelemetry-demo-ad/bin/Ad"]
