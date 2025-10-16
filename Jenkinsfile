node {
  
  currentBuild.result = 'SUCCESS'

  try {
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

  } catch (e) {
    currentBuild.result = 'FAILURE'
    throw e

  } finally {
    if (currentBuild.result == 'SUCCESS') {
      mail to: 'ofeurekondo@gmail.com',
           from: 'ofeurekondo@gmail.com',
           subject: "✅ Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Build succeeded. ${env.BUILD_URL}GOOD JOB"
    } else {
      mail to: 'ofeurekondo@gmail.com',
           from: 'ofeurekondo@gmail.com',
           subject: "❌ Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Build failed. ${env.BUILD_URL}NOT GOOD JOB BUT EMAILS work"
    }
  }
}
