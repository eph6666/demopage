pipeline {
    agent any
    stages {
        stage("git") {
            steps {
                sh 'git clone https://github.com/eph6666/demopage.git'
            }
        }
    },
    stages {
        stage("pre-build") {
            steps {
                sh 'sed -i "s/###/$BUILD_NUMBER/g" demopage/application.yaml'
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
                sh 'kubectl apply -f demopage/application.yaml'
            }
        }
    },
}