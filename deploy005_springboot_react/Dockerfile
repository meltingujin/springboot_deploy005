# github actions를 사용할 때 steps > uses가 해준다

# # 1단계: 실행 환경만 준비 (maven을 통한 빌드 Java 21 jdk)
# FROM maven:3.9.11-eclipse-temurin-21 AS build
# WORKDIR /app

# # 라이브러리 캐싱(pom.xml 변경이 없으면 이 단계는 캐시된것을 사용하겠다)
# COPY pom.xml .
# RUN mvn dependency:go-offline

# # 소스 복사 및 패키징
# COPY src ./src
# RUN mvn clean package -DskipTests

# 2단계 : 실행환경(java 21 JRE)
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app

# COPY --from=build /app/target/*.jar app.jar
COPY target/*.jar app.jar

# 서버 포트 노출
EXPOSE 9090

# 타임존 설정 및 실행
ENTRYPOINT ["java", "-jar", "-Duser.timezone=Asia/Seoul", "app.jar"]
