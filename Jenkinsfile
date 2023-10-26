    stage('Cloning Git') {
        /* Making sure we have repository cloned to workspace */
        checkout scm
    }

    stage('Build-and-Tag') {
        /* This builds the actual image, and it is synonymous to docker build on cmd line */
      app = docker.build("lopdave/real-estate")
    }

    stage('Post-to-dockerhub') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push("latest")
        }
    }

    stage('Pull-image-server') {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}
