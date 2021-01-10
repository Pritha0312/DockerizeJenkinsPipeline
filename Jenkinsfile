def CONTAINER_NAME="jck1"
def CONTAINER_TAG="latest"
def USERNAME="00000012"
def PASSWORD="Pritha@03"


node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def docker = "mydocker"
    def registry = '00000012'
    def registryCredential = '00000012'
    def dockerImage = ''
    
	
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
	
	

   stage('Push to Docker Registry'){
        withCredentials([usernamePassword(credentialsId: '00000012', usernameVariable: '00000012', passwordVariable: 'Pritha@03')]) {
            pushToImage(CONTAINER_NAME, CONTAINER_TAG, USERNAME, PASSWORD)
        }
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
def imageBuild(containerName, tag){
    sh "docker build -t $containerName:$tag ."
    echo "Image build complete"
}
def pushToImage(containerName, tag, dockerUser, dockerPassword){
    sh "docker login -u $dockerUser -p $dockerPassword"
    sh "docker tag $containerName:$tag $dockerUser/$containerName:$tag"
    sh "docker push $dockerUser/$containerName:$tag"
    echo "Image push complete"
}


	
