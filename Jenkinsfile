pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Sumitshukla4020/etpprac'
        BRANCH = 'master'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                bat 'docker build -t static-html-site .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f html-container || echo no container to remove'
                bat 'docker run -d -p 8085:80 --name html-container static-html-site'
            }
        }
    }

    post {
        success {
            echo 'Static HTML site deployed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
