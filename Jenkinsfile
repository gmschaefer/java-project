properties([pipelineTriggers([githubPush()])])

node('linux') {
  git url: 'https://github.com/gmschaefer/java-project.git', branch: 'master'
  stage('Unit Tests') {
    sh "ant -f test.xml -v"
  }
  
  stage('Build') {
    sh "ant -f build.xml -v"
  }
 
  stage('Deploy') {
    sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://assign10-deploy/"
  }
 
  stage('Report') {
    sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
  }
}

