node {
    def app
    stage('Clone repository') {
        checkout scm
    }

    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
                app = docker.build("dariyozz/jenkins-blueocean")
        }

        stage('Push image') {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        echo "Skipping Docker build and push as the branch is not 'dev'."
    }
}
