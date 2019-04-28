properties([pipelineTriggers([githubPush()])])

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/Shortreed1987/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/*.xml'
    }
    
}
