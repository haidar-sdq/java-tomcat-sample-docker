pipeline {
    agent any
    environment {     
    registry = "haidarsdq/hubimage1"
    registryCredential = 'docker_cred'
    dockerImage = ''
    }
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
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        
    }
}
