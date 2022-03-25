pipeline {
    agent any
    stages {
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/haidar-sdq/java-tomcat-sample-docker.git' 
            }
        } 
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
                sh 'docker login -u haidarsdq -p *znj!f9xCS@.kNE'
                echo 'Login completed'
                sh 'sudo docker push haidarsdq/hubimage1:${env.BUILD_ID}'           
                echo 'Push Image Completed'
    }
}
        
    }
}
