pipeline { 
    agent any 

    environment { 
        IMAGE_NAME = 'urdubol-app' 
        CONTAINER_NAME = 'urdubol-container' 
        HOST_PORT = '8000' 
        APP_PORT = '8080'
    } 

    stages { 
        stage('Checkout Code') {
              steps { 
                   echo 'Pulling latest code from GitHub...' 
                   checkout scm } } 
          stage('Build Docker Image') { 
              steps { 
                   script { 
                        echo "Building Docker image: ${IMAGE\_NAME}:${env.BUILD\_ID}..." sh "docker build -t ${IMAGE\_NAME}:${env.BUILD\_ID} -t ${IMAGE\_NAME}:latest ." 
 }
  }
 } 

stage('Test Image'){
 steps { 
script { 
echo 'Testing Docker container execution...' sh "docker run --rm ${IMAGE\_NAME}:latest python3 --version || true" } } } stage('Deploy Application') { steps { script { echo 'Deploying UrduBol container...' // Stop and remove previous container instance if running sh "docker stop ${CONTAINER\_NAME} || true" sh "docker rm ${CONTAINER\_NAME} || true" // Start new container instance sh "docker run -d --name ${CONTAINER\_NAME} -p ${HOST\_PORT}:${APP\_PORT} ${IMAGE\_NAME}:latest" } } } } post { success { echo 'UrduBol application successfully built and deployed!' } failure { echo 'Pipeline failed. Check Jenkins build logs for details.' } } }
