pipeline {
    agent any
    environment {     
    DOCKERHUB_CREDENTIALS= credentials('docker_cred')     
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh "sudo docker login -u haidarsdq -p $DOCKERHUB_CREDENTIALS"
                echo 'Login completed'
                sh 'sudo docker push haidarsdq/hubimage1:${env.BUILD_ID}'           
                echo 'Push Image Completed'
    }
}
    }
}
