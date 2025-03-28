node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("dariyozz/jenkins-blueocean")
    }
    stage('Push image') {
            docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}


