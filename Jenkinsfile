pipeline {
    
    agent any
    
    environment {
       REGISTRY='mauron'
       DOCKERHUB_CREDENTIALS = credentials('dockerhub')
       DOCKER_USER=credentials('docker-user')
       DOCKER_PWD=credentials('docker-pwd')
       JAVA_HOME= tool 'jdk21'
       MAVEN_HOME= tool 'm3' 
    }
    
    stages {
        stage('Clonar Repositorio') {
            steps {
                script {
         
                  def repo = 'https://github.com/gmacastil/ms-agosto-01.git'
    
                  git(
                    url: repo,
                    branch: 'main',
                    credentialsId: 'github-token'
                  )
                }
            }
        }
        
        
        stage('Compilar con Maven') {
            steps {
                script {
                    sh "echo $JAVA_HOME"
                    sh "$MAVEN_HOME/bin/mvn clean package -DskipTests"
                }
            }
        }
        
        stage('Análisis SonarQube') {
            steps {
                script {
                    withSonarQubeEnv('sonar') {
                        sh "$MAVEN_HOME/bin/mvn sonar:sonar"
                    }
                }
            }
        }
        
         stage('Construir y Publicar Imagen Docker') {
            steps {
                script {
                  sh 'docker build . -t $REGISTRY/ms-agosto-01:$BUILD_ID'
                  sh 'echo $DOCKER_PWD | docker login -u $DOCKER_USER --password-stdin'
                  sh 'docker push $REGISTRY/ms-agosto-01:$BUILD_ID'
                 
                }
            }
        }

        stage('Limpiar Workspace') {
            steps {
                cleanWs()
            }
        }
        
        

    }
}