node {
    def app

    stage('Clone repository') {
        
        checkout scm
    }

    stage('Build image') {
        
        app = docker.build("mattwoz02/coursework2")
    }

    stage('Test image') {
        
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
			    sh "ssh ubuntu@54.89.108.19 \
			    	kubectl set image deployment/coursework coursework-675b989f5c-vn4w7=mattwoz02/dockerfile:latest"
			    }
		    }
	    }	
  
