node{
    
    stage('Get repo') {
  
        checkout scm
    }

       
    stage('Build docker image') {
	script{
        app = docker.build("mattwoz02/coursework2")
}
    }

    stage('Push image to Dockerhub') {
            docker.withRegistry('https://registry.hub.docker.com', 'mattwoz02') {
            	docker.image('dockerfile:latest').push()
            
        }
    }
}
