def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, cloud: 'kubernetes', containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'kubectl', image: 'k3integrations/kubectl', ttyEnabled: true, command: 'cat'),
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
                git 'https://github.com/jenkinsci/kubernetes-plugin.git'
                stage('Config') {
                    sh 'pwd'
                    sh 'sed -i "s/###/$BUILD_NUMBER/g" demopage/application.yaml'
                }
                stage('Deploy') {
                    sh 'kubectl apply -f demopage/application.yaml'
                }
            }
        }
    }
}