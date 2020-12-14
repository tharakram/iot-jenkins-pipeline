def genericSh(cmd) {
  if (isUnix()) {
    sh cmd
  }
  else {
    bat cmd
  }
}

node {
  stage('Checkout') {
    checkout scm
    echo "Checkout complete"
  }

  stage('Build') {
    echo "Build started"
    sh pwd
    sh ls
    echo "Build complete"
  }
  
  stage('Push') {
    echo "Pushing the image to container"
    azureIoTEdgePush dockerRegistryType: 'acr', dockerRegistryEndpoint: [credentialsId: 'az-tharak-service-principal', url: 'tharak.azurecr.io'], bypassModules: '', resourceGroup: 'iot-hub-tharak-rg', defaultPlatform: 'amd64', deploymentManifestFilePath: 'deployment.template.json'
  }

  stage('Deploy') {
    azureIoTEdgeDeploy azureCredentialsId: 'az-tharak-service-principal', deploymentId: 'jenkins-deploy', deploymentType: 'single', deviceId: 't-rpi-4', iothubName: 'iot-hub-tharak-one', priority: '0', resourceGroup: 'iot-hub-tharak-rg', rootPath: './', targetCondition: ''
  }
}
