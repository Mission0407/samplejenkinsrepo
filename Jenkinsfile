node('maven'){
  def mvnhome = tool name: 'maven361', type: 'maven'
  stage('checkout'){
  git 'https://github.com/Mission0407/samplejenkinsrepo.git'
}
  stage('build'){
    sh "${mvnhome}/bin/mvn clean test"
  }
}
