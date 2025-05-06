pipeline{
    agent any
    Environment {
        GIT_REPO: 
        BRANCH: 'master'
    }
    stages{
        stage('Clone'){
            steps{
                git branch: "${BRANCH}", url:"${GIT_REPO}"
            }
        }
        stage('Build'){
            steps{
                bat 'docker build -t static-html-site .'
            }
        }
        stage('Deploy'){
            steps{
                bat 'docker rm -f html-container || echo "no container to remove"'
                bat 'docker run -d -p 8085:80 --name html-container static-html-site'
            }
        }
    }
    post{
        success{
            echo 'static html site deployed successfullly!'
        }
        failure{
            echo 'pipeline failed!'
        }
    }
}