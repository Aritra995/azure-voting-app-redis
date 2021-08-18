pipeline{
    agent any
    stages{
        //implicit checkout
        stage('Verify Branch'){
            steps{
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build'){
            steps{
                sh '''cd azure-vote/
                    sudo docker build -t jenkins-pipeline .
                    sudo docker images -a
                    cd ..'''
            }
        }
    }
    post{
        always{
            emailext subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}",
                body: "Please go to ${BUILD_URL} and verify the build", 
                attachLog: true, 
                compressLog: true, 
                to: "test@jenkins",
                recipientProviders: [upstreamDevelopers(), requestor()]
        }
    }
}