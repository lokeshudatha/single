pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-cred')
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
                            sh 'sudo docker build -t 9515524259/python_image:latest .'
                        }
                    }
                }

                stage('Build Java Image') {
                    steps {
                        dir('java') {
                            sh 'sudo docker build -t 9515524259/java_image:latest .'
                        }
                    }
                }
                
                stage('Build Nginx Image') {
                    steps {
                        dir('nginx') {
                            sh 'sudo docker build -t 9515524259/nginx_image:latest .'
                        }
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh """
                    sudo docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                    sudo docker push 9515524259/python_image:latest
                    sudo docker push 9515524259/java_image:latest
                    sudo docker push 9515524259/nginx_image:latest
                """
            }
        }
    }
}
