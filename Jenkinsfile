node('maven'){
  def mvnhome = tool name: 'maven360', type: 'maven'
  stage('checkout'){
    git credentialsId: 'github-passwd', url: 'https://github.com/deepaklama0815/samplejenkinsrepo.git'
  }
  stage('test'){
      sh "${mvnhome}/bin/mvn clean test surefire-report:report-only"
      junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
      archiveArtifacts allowEmptyArchive: true, artifacts: 'target/surefire-reports/*'
  }
  stage('package'){
      sh "${mvnhome}/bin/mvn clean package -Dskiptest"
  }
}
