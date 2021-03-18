def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, cloud: 'kubernetes', containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'kubectl', image: 'k3integrations/kubectl', ttyEnabled: true, command: 'cat'),
  ]) {

    node(label) {
        stage('Build') {
            git 'https://github.com/eph6666/demopage.git'
            container('maven') {
                stage('Build-1') {
                    sh 'mvn -version'
                    sh 'ls'
                }
            }
        }
        stage('Deploy') {
            git 'https://github.com/eph6666/demopage.git'
            container('kubectl') {
                stage('Config') {
                    sh 'sed -i "s/###/$BUILD_NUMBER/g" demopage/application.yaml'
                }
                stage('Deploy') {
                    sh 'kubectl apply -f demopage/application.yaml'
                }
            }
        }
    }
}