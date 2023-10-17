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
        
        stage ("Generate spring-angular springboot image") {
            steps {
                dir("springboot"){ 
                    sh "mvn clean install"
                    sh "docker build -t springboot:latest ."
                }
            }
        }
        
        stage ("Generate spring-angular angular-app image") {
            steps {
                dir("angular-app"){ 
                    sh "npm install"
                    sh "npm run build --prod"
                    sh "docker build -t angular-app:latest ."
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
