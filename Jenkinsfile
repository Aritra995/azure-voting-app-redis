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
                sh 'docker images -a'
                sh """ 
                    cd azure-vote/
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                """
            }
        }
    }
}