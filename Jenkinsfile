pipeline {
    agent {
        node {
            label 'docker-remote-agent-staging'
        }
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        timestamps()
        buildDiscarder logRotator(daysToKeepStr: '15', numToKeepStr: '10')
        ansiColor('xterm')
    }

    stages {
        stage("Preparation") {
            steps {
                checkout scm
                echo '###### ENVIRONMENT VARIABLES - BEGIN ######'
                sh 'printenv | sort'
                echo '###### ENVIRONMENT VARIABLES - END ######'
                
            }
        }
        stage("Build") {
            steps {
                sh 'build-wrapper --out-dir bw-outputs ./build.sh'
            }
        }
        stage("Scan") {
            steps {
                sh 'sonar-scanner'
            }
        }
    }

    post {
        always {
            echo "Post - always"
        }
        success {
            echo "Post - success"
        }
        unstable {
            echo "Post - unstable"
        }
        failure {
            echo "Post - failure"
        }
    }
}