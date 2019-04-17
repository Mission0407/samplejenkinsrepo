node('maven'){
  def mvnhome = tool name: 'maven361', type: 'maven'
  stage('checkout'){
  git 'https://github.com/Mission0407/samplejenkinsrepo.git'
}
  stage('build'){
    sh "${mvnhome}/bin/mvn clean test surefire-report:report-only"
    archiveArtifacts 'target/surefire-reports/*'
    junit 'target/surefire-reports/*.xml'
    publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
  }
  stage('package'){
    sh "${mvnhome}/bin/mvn package -DskipTests=true"
  }
  stage('deployment'){
    sshagent(['anonym-key']) {
    sh "scp -o StrictHostKeyChecking=no /home/ec2-user/jenkins_ws/workspace/sample-pipeline/target/my-app-1-RELEASE.jar ec2-user@54.80.174.77:/home/ec2-user/"
}
}
