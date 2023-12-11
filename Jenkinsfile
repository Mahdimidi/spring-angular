pipeline {
    agent any
    tools {
        maven 'maven'
        nodejs 'node'
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
        
        stage ("Generate spring-angular/springboot/app image") {
            steps {
                dir("spring-angular/springboot/app"){ 
                    sh "mvn clean install"
                    sh "docker build -t springboot ."
                }
            }
        }
        
        stage ("Generate spring-angular/angular-app image") {
            steps {
                dir("spring-angular/angular-app"){ 
                    sh "docker build -t angular-app ."
                }
            }
        }
        
        stage ("Run docker compose") {
            steps {
                dir("spring-angular"){
                    sh "docker compose up -d "
                }
            }
        }
    }                        
}
