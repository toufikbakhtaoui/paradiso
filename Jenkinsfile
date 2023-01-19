pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'jdk17'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
                archive 'target/*.jar'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Sonar') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar \
                -Dsonar.projectKey=paradiso \
                -Dsonar.host.url=http://localhost:9000'
                }
            }
        }
    }
}
