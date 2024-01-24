pipeline {
  agent any
  stages {
    stage('Running tests') {
      steps {

        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
          sh 'chmod +x gradlew'
          sh './gradlew clean test -PincludeTags="${tags}"'
        }
      }
    }
    stage('Publish Report') {
      steps {
        publishReport()
      }
    }
    stage('Publish Excel') {
          steps {
            publishExcel()
          }
      }
  }
}

def publishReport() {
  publishHTML(target: [
    reportName: 'Valoration E2E Test Results',
    reportDir: 'target/site/serenity',
    reportFiles: 'index.html',
    keepAll: true,
    alwaysLinkToLastBuild: true,
    allowMissing: false
  ])
}
def publishExcel() {
  archiveArtifacts artifacts: 'src/test/resources/dataTest/test.xlsx', allowEmptyArchive: true
}