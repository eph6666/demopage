pipeline {
    agent any

    stages {
        stage("pre-build") {
            steps {
                sh 'sed -i "s/###/$BUILD_NUMBER/g" application.yaml'
            }
        }
    },
    stages {
        stage("pre-build") {
            steps {
                sh 'echo "Build"'
            }
        }
    },
    stages {
        stage("deploy") {
            steps {
                sh 'kubectl apply -f application.yaml'
            }
        }
    },
}