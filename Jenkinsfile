pipeline {
    agent any 
    tool {
        tool-maven
    }
    stages {
        stage("build the jar") {
            steps {
                script {
                    echo "building the application "
                    sh "mvn package" 
                }
            }
        }
            stage("build the image") {
                steps {
                    script {
                        echo "building the image..."
                        withcrenditials([usernamepassword(credentialId: "docker-hub-repo", passwordVariable: "PASS" , usernamVariable:"USER" )]){
                            sh" docker build -t wimetirix/demo-app:v1 ."
                            sh" echo $PASS | docker login -u $USER --password-stdin"
                            sh "docker push wimetirix/demo-app:v1 "

                        }
                    }
                }
            }
            stage('deploy the image') {
                steps {
                    script {
                        echo "deploying the image.."
                    }
                }
            }
    }   

}