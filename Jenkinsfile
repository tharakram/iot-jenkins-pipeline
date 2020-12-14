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
    azureIoTEdgePush dockerRegistryType: 'acr', acrName: 'tharak', bypassModules: '', azureCredentialsId: 'az-tharak-service-principal', resourceGroup: 'iot-hub-tharak-rg', rootPath: './'
    echo "Build complete"
  }

  stage('Deploy') {
    azureIoTEdgeDeploy azureCredentialsId: 'az-tharak-service-principal', deploymentId: 'jenkins-deploy', deploymentType: 'single', deviceId: 't-rpi-4', iothubName: 'iot-hub-tharak-one', priority: '0', resourceGroup: 'iot-hub-tharak-rg', rootPath: './', targetCondition: ''
  }
}
