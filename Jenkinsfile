def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, cloud: 'kubernetes') {
    node(label) {
        stage('git') {
            sh 'git clone https://github.com/eph6666/demopage.git'
        },
        stage('pre-build') {
            sh 'sed -i "s/###/$BUILD_NUMBER/g" demopage/application.yaml'
        },
        stage('build') {
            sh 'echo "Build"'
        },
        stage('deploy') {
            sh 'kubectl apply -f demopage/application.yaml'
        }
    }
}