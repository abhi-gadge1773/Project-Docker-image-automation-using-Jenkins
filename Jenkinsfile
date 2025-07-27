pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Piyushbankhede/Project-Docker-image-automation-using-Jenkins.git'
            }
        }
        
        stage('Build Image') {
            steps {
                script {
                    docker.build("localhost:5000/piyushankhede-jenkins-apache:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Push to Registry') {
            steps {
                script {
                    docker.withRegistry('http://localhost:5000') {
                        docker.image("localhost:5000/piyushbankhede-jenkins-apache:${env.BUILD_ID}").push()
                    }
                }
            }
        }
        
        stage('Deploy Container') {
            steps {
                script {
                    // Cleanup old container if exists
                    sh 'docker rm -f piyushbankhede-jenkins-apache || true'
                    
                    // Run new container (mapping host port 8088 to container port 8088)
                    sh """
                    docker run -d \
                        --name piyushbankhedeh-jenkins-apache \
                        -p 8088:8088 \
                        localhost:5000/piyushbankhede-jenkins-apache:${env.BUILD_ID}
                    """
                    
                    // Verify deployment
                    sh 'curl -I http://localhost:8088'
                }
            }
        }
    }
}
