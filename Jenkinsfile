node('maven'){
  def mvnhome = tool name: 'maven361', type: 'maven'
  stage('checkout'){
  git 'https://github.com/Mission0407/samplejenkinsrepo.git'
}
  stage('build'){
    sh "${mvnhome}/bin/mvn clean test surefire-report:report-only"
    archiveArtifacts 'target/surefire-reports/*'
    //junit allowEmptyResults: true, testResults: 'target/surefire-reports/'junit 'target/surefire-reports/*.xml'
    junit 'target/surefire-reports/*.xml'
  }
  stage('package'){
    sh "${mvnhome}/bin/mvn package -DskipTests=true"
  }
}
