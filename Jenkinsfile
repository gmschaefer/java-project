properties([pipelineTriggers([githubPush()])])

node('linux') {
  git url: 'https://github.com/gmschaefer/java-project.git', branch: 'master'
  stage('Unit Tests') {
    ant -f test.xml -v
  }
  
  stage('Build') {
    ant -f build.xml -v    
  }
 
  stage('Deploy') {
    aws s3 cp rectangle*jar s3://assign10-deploy/    
  }
 
  stage('Report') {
    aws cloudformation describe-stask-resources --region us-east-1 stack-name jenkins
  }
}

