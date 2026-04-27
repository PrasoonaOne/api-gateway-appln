pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/PrasoonaOne/api-gateway-appln.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t gateway-image .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker stop gateway-container || true'
                sh 'docker rm gateway-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name gateway-container \
                -p 8081:8081 \
                gateway-image
                '''
            }
        }
    }
}
