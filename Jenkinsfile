node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def docker = "mydocker"
    def registry = '00000012/dockerize_jenkins'
    def registryCredential = '00000012'
	
	stage('Git') {
		git 'https://github.com/Pritha0312/DockerizeJenkinsPipeline.git'
	}
	stage('Build') {
		sh 'npm install'
		sh 'npm run bowerInstall'
	}
	stage('Test') {
		sh 'npm test'
	}
	/*stage('Building image') {
        docker.withRegistry( 'https://hub.docker.com/repository/docker/00000012/dockerize_jenkins') {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }*/
	stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://hub.docker.com/repository/docker/' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
