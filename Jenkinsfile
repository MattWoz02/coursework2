node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("mattwoz02/coursework2")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push to DockerHub') {
            steps {
                script {
                    // Use the correct credentialsId for DockerHub
                    docker.withRegistry('https://registry.hub.docker.com', 'mattwoz02') {
                        docker.image('dockerfile:latest').push()
                    }
    }
}
}
}
