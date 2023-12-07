pipeline {
    agent any
    tools{
        nodejs 'npm'
    }
    environment{
        MY_IMAGE='react-image'
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t ${MY_IMAGE} .'
            }
        }
        stage('Test') {
            steps {
                echo "Testing .... dg mix teh"
            }
        }
        stage('Deploy') {
            steps {
                script{
                def existImageID= sh(script: 'docker ps -aq -f name="${MY_IMAGE}"',returnStdout:true)
                    echo "ExistImageID:${existImageID}"
                    if(existImageID){
                        echo '${existImageID} is removing ...'
                        sh 'docker rm -f ${MY_IMAGE}'
                    }else{
                        echo 'No existing container'
                    }
                }
                sh 'docker run -d -p 3000:3000 --name ${MY_IMAGE} ${MY_IMAGE}'
            }
        }
    }
}