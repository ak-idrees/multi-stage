pipeline {
    agent any 

    tools {
       maven "tool-maven-3.9.12"
    }

    stages {
        stage("build the jar") {
            steps {
                script {
                    echo "building the application"
                    sh "mvn package"
                }
            }
        }

        stage("build the image") {
            steps {
                script {
                    echo "building the image..."
                    withCredentials([usernamePassword(
                        credentialsId: "docker-hub-repo",
                        usernameVariable: "USER",
                        passwordVariable: "PASS"
                    )]) {
                        sh "docker build -t wimetirix/demo-app:v1 ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push wimetirix/demo-app:v1"
                    }
                }
            }
        }

        stage('deploy the image') {
            steps {
                script {
                    echo "deploying the image..."
                }
            }
        }
    } // closes stages
} // closes pipeline
