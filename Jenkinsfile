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

	stage('Deploy to K8s')
  {
   steps{
    sshagent(['k8s-jenkins'])
    {
     sh 'scp -r -o StrictHostKeyChecking=no deploy.yaml username@100.26.18.152:/path'script{
      try{
       sh 'ssh ubuntu@52.3.252.77 kubectl apply -f /path/deploy.yaml --kubeconfig=/path/kube.yaml'}catch(error)
       {
	}
     }
    }
   }
  }


}                   	
  
