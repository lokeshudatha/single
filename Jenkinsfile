pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-creds')
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Images in Parallel') {
            parallel {
                stage('Build Python Image') {
                    steps {
                        dir('python') {
                            sh 'docker build -t 9515524259/python_image:latest .'
                        }
                    }
                }

                stage('Build Java Image') {
                    steps {
                        dir('java') {
                            sh 'docker build -t 9515524259/java_image:latest .'
                        }
                    }
                }
                
                stage('Build Nginx Image') {
                    steps {
                        dir('nginx') {
                            sh 'docker build -t 9515524259/nginx_image:latest .'
                        }
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh """
                    docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                    docker push 9515524259/python_image:latest
                    docker push 9515524259/java_image:latest
                    docker push 9515524259/nginx_image:latest
                """
            }
        }
    }
}
