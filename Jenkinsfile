pipeline {
    agent any
    stages {
        stage('Build BackEnd') {
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Deploy Backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        } 
        stage('API Test') {
            steps {
                dir('api-test') {
                    git credentialsId: 'GitHub_Login', url: 'https://github.com/JoaoVitorVictorio/Integracao_Continua_Api.git'
                    bat 'mvn test'
                }
            }
        }
    }
}
