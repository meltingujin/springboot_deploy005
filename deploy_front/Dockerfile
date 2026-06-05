# # 1단계: 실행 환경만 준비 (Nginx)
# FROM nginx:stable-alpine

# # GitHub Actions에서 이미 빌드된 dist 폴더를 Nginx의 정적 파일 경로로 복사
# # (Vite 기준 dist, Create React App 기준 build 폴더)
# COPY dist /usr/share/nginx/html

# # 핵심: 작성하신 nginx.conf를 Nginx 설정 디렉토리로 복사
# #COPY nginx.conf /etc/nginx/conf.d/default.conf

# # Nginx 기본 포트
# EXPOSE 80

# # Nginx 실행
# CMD ["nginx", "-g", "daemon off;"]

####################################################

# # Nginx를 사용하지 않고, 로컬에서 실행시켰던 방식으로 npm run dev를 사용하는 방법
# FROM node:24-alpine

# WORKDIR /app

# # package.json을 복사해서 실행 => node_modules가 만들어짐
# COPY .. 
# RUN npm install
# EXPOSE 5173
# # 접근허용
# CMD [ "npm", "run", "dev", "--", "--hose" ]

######################################################
# #1단계 : 빌드
# FROM node:24-alpine AS build
# WORKDIR /app

# # package.json을 통해서 의존성(패키지) 설치
# COPY package.json ./
# RUN npm install

# # 소스코드 복사
# COPY . .
# # React 빌드 수행(dist 폴더 생성)
# RUN npm run build

# 2단계 : 실행환경(Nginx 환경 연결)
FROM nginx:stable-alpine

# React의 빌드 결과물을 Nginx 정적폴더로 복사
# COPY --from=build /app/dist /usr/share/nginx/html
COPY dist /usr/share/nginx/html

# Nginx기본 설정 대신에 사용할 설정파일이 있다면 추가로 Copy해주면 된다
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
# nginx를 실행하면 백그라운드 실행. nginx를 컨테이너가 종료되도 실행될 수 있도록
CMD ["nginx", "-g", "daemon off;"]