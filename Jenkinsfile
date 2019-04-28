pipeline{
    agent any
    stage('Unit Tests'){
        sh 'ant -f test.xml -v'
        junit 'reports/*.xml'
    }
}
