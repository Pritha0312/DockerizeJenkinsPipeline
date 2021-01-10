node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def docker = "mydocker"
    def registry = '00000012'
    def registryCredential = '00000012'
    def dockerImage = ''
    def CONTAINER_NAME="jck1"
    def CONTAINER_TAG="latest"
	
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
        docker.withRegistry( registryCredential) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}*/
	stage('Image Build'){
        imageBuild(CONTAINER_NAME, CONTAINER_TAG)
    }
	
	def imageBuild(containerName, tag){
    sh "docker build -t $containerName:$tag  -t $containerName --pull --no-cache ."
    echo "Image build complete"
}
	
	stage('Build image') {
      
          dockerImage = docker.build registry
        
      
    }
	
	/*stage('Registring image') {
        docker.withRegistry( 'https://hub.docker.com/repository/docker/' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}*/
    /*stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }*/
    
}
