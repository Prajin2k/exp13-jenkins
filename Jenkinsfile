pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building Application'

                sh 'mkdir -p build'
                sh 'cp index.html build/index.html'

                echo 'Build Successful'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Application'

                sh 'test -f build/index.html'

                sh "grep -q 'Welcome to Jenkins CI/CD Pipeline' build/index.html"

                echo 'All Tests Passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Application'

                sh 'mkdir -p "$JENKINS_HOME/deployed-site"'

                sh 'cp build/index.html "$JENKINS_HOME/deployed-site/index.html"'

                echo 'Deployment Successful'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Completed Successfully!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}
