node {
   stage('Preparation') {
      // Get some code from a GitHub repository
      git 'https://github.com/formulahendry/EdgeSolutionJenkinsTest'
   }
   stage('Build') {
      azureIoTEdgeBuild defaultPlatform: 'amd64', deploymentManifestFilePath: 'deployment.template.json'
   }
   stage('Push') {
      azureIoTEdgePush acrName: 'aziotedgedevclitest', azureCredentialsId: 'JunServicePrincipal', defaultPlatform: 'amd64', deploymentManifestFilePath: 'deployment.template.json', resourceGroup: 'azure-iot-edge'
   }
   stage('Generate Deployment Manifest') {
      azureIoTEdgeGenConfig defaultPlatform: 'amd64', deploymentFilePath: 'config/deployment.json', deploymentManifestFilePath: 'deployment.template.json'
   }
   stage('Deploy') {
      azureIoTEdgeDeploy azureCredentialsId: 'JunServicePrincipal', deploymentFilePath: 'config/deployment.json', deploymentId: "deploy00${env.BUILD_NUMBER}", deploymentType: 'single', deviceId: 'py-sample', iothubName: 'azure-iot-toolkit-test', priority: '10', resourceGroup: 'azure-iot-edge', targetCondition: ''
   }
}