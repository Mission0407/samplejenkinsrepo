node('maven'){
  def mvnhome = tool name: 'maven360', type: 'maven'
  stage('checkout'){
    git credentialsId: 'github-passwd', url: 'https://github.com/deepaklama0815/samplejenkinsrepo.git'
  }
  stage('test'){
      sh "${mvnhome}/bin/mvn clean test surefire-report:report-only"
      junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
      archiveArtifacts allowEmptyArchive: true, artifacts: 'target/surefire-reports/*'
      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
  }
  stage('package'){
      sh "${mvnhome}/bin/mvn clean package -Dskiptest"
  }
  stage('deployment'){
      sshagent(['new-machine']) {
    sh "scp -o StrictHostKeyChecking=no /home/ec2-user/workspace/new-work/target/my-app-1-RELEASE.jar ec2-user@54.236.4.88:/home/ec2-user/"
  }
  }
}
