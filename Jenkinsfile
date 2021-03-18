def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, cloud: 'kubernetes', serviceAccount: 'jenkins', containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'kubectl', image: '111706684826.dkr.ecr.us-east-1.amazonaws.com/library/debug:latest', ttyEnabled: true, command: 'cat'),
  ]) {

    node(label) {
        stage('Build') {
            container('maven') {
                stage('Build-1') {
                    sh 'mvn -version'
                    sh 'ls'
                }
            }
        }
        stage('Deploy') {
            container('kubectl') {
                git branch: 'main', url: 'https://github.com/eph6666/demopage.git'
                stage('Config') {
                    sh 'ls'
                    sh 'sed -i "s/###/$BUILD_NUMBER/g" application.yaml'
                }
                stage('Deploy') {
                    sh 'kubectl auth can-i create cm'
                    sh 'kubectl auth can-i create svc'
                    sh 'kubectl auth can-i create deployment'
                    sh 'kubectl apply -f application.yaml'
                }
            }
        }
    }
}