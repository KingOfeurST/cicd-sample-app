ode {
  stage('Preparation') {
    catchError(buildResult: 'SUCCESS') {
      sh 'docker stop samplerunning'
      sh 'docker rm samplerunning'
    }
  }
  stage('Build') {
    build job: 'BuildSampleApp'
  }
  stage('Results') {
    build job: 'TestSampleApp'
  }
}