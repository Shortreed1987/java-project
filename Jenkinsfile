properties([pipelineTriggers([githubPush()])])

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/Shortreed1987/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/*.xml'
    }
    stage('Build'){
        git 'https://github.com/Shortreed1987/java-project.git'
        sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'fce4d37d-d3e7-4ac7-ab25-0236467df05e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws s3 cp /workspace/java-pipeline/dist/*.jar s3://seis66503-shortreed/'
        }
    }
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'fce4d37d-d3e7-4ac7-ab25-0236467df05e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describestack-resources --region us-east-1 --stack-name jenkins'
        }
    }
}
