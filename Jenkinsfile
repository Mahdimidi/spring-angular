pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage ("Clean up"){
            steps {
                deleteDir()
            }
        }
        
        stage ("Clone repo"){
            steps {
                sh "git clone https://github.com/Mahdimidi/spring-angular.git"
            }
        }
        
        stage ("Generate spring-angular backend image") {
            steps {
                dir("back-spring"){ 
                    sh "mvn clean install"
                    sh "docker build -t back-spring:latest ."
                }
            }
        }
        
        stage ("Generate spring-angular frontend image") {
            steps {
                dir("front-angular"){ 
                    sh "npm install"
                    sh "npm run build --prod"
                    sh "docker build -t front-angular:latest ."
                }
            }
        }
        
        stage ("Run docker compose") {
            steps {
                dir("spring-angular"){
                    sh "docker-compose up -d"
                }
            }
        }
    }                        
}
