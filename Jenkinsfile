pipeline {
    agent any
    
    tools {
        maven 'localMaven'
    }
    
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/lionelfalcon/maven-project.git', credentialsId: 'cred4github'
            }
        }
        
        stage('Compile') {
            steps {
                withMaven(maven: 'localMaven') {
                    bat 'mvn compile'
                }
            }
        }
        
        stage('Test') {
            steps {
                withMaven(maven: 'localMaven') {
                    bat 'mvn test'
                }
            }
        }
        
        stage('Build') {
            steps {
                withMaven(maven: 'localMaven') {
                    bat 'mvn -B -DskipTests clean package'
                }
            }
        }
        
        stage('Build and send Results Sonar') {
            steps {
                withSonarQubeEnv(installationName: 'localSonarQube', credentialsId: 'key4sonarqube') {
                    bat 'mvn -B -DskipTests clean package sonar:sonar'
                }
            }
        }
    }
}
