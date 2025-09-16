# CI

## compilar

mvn package

## run

java -jar nombre-artefacto.jar

## construir la imagen

docker build . -t nombre-repo:TAG

docker build . -t ms-agosto-01:v3

docker build . -t server-registry/nombre-repo:TAG


## tag + push

docker tag nombre-repo:TAG server-registry/nombre-repo:TAG

docker tag ms-agosto-01:v3 mauron/ms-agosto-01:v3
docker push mauron/ms-agosto-01:v3

// Login a la nube

docker login server-registry

docker push server-registry/nombre-repo:TAG

# docker

docker run --name ms-agosto-01-dev -d -p 9090:8888 mauron/ms-agosto-01:v2


# dev
docker run --name ms-agosto-01-dev -d -p 9090:8888 -e MESSAGE="hola equipo desarrollo" mauron/ms-agosto-01:v3


# qa
docker run --name ms-agosto-01-qa -d -p 9091:8888 -e MESSAGE="hola calidad" mauron/ms-agosto-01:v3


# prd
docker run --name ms-agosto-01-prd -d -p 9092:8888 -e MESSAGE="hola prod" mauron/ms-agosto-01:v3

# Docker compose

docker compose up -d


sonar url: http://localhost:9001
sonar token: squ_7665578e41538f3b3a7438ee18500f39b107c8e8


mvn clean verify sonar:sonar \
  -Dsonar.projectKey=ms-agosto-01 \
  -Dsonar.projectName=ms-agosto-01 \
  -Dsonar.host.url=http://localhost:9001 \
  -Dsonar.token=squ_7665578e41538f3b3a7438ee18500f39b107c8e8



# jenkins


cd docker/jenkins
docker compose up -d

