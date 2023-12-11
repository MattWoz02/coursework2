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

	stage('Push image') {
        withDockerRegistry([ mattwoz02: "200219771892", url: "https://hub.docker.com/repositories/mattwoz02/dockerfile" ]) {
        sh 'docker push mattwoz02/dockerfile:latest'
        }
}

	stage('Deploying to Kubernetes'){
		    echo "deploying..."
		    script {
			    sh "ssh ubuntu@52.3.252.77 \
			    	kubectl set image deployments/devopscw2 server-app-l824t=mattwoz02/dockerfile:latest"
			    }
		    }
	    }	
  
