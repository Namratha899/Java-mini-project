pipeline {

    agent any

    stages {

        stage('Determine Version') {
            steps {
                script {
                    env.APP_VERSION = "v${BUILD_NUMBER}"

                    echo "Jenkins Build Number: ${BUILD_NUMBER}"
                    echo "Application Version: ${APP_VERSION}"
                }
            }
        }

    stage('Checkout Version') {
            steps {
                sh """
                    git fetch --tags --force
                    git checkout ${APP_VERSION}
                """

                echo "Checked out application version: ${APP_VERSION}"
            }
        }



        stage('Build') {
            steps {
                dir('sample-app') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy') {
            steps {
                dir('sample-app') {

                    echo "Deploying Application Version: ${APP_VERSION}"

                    sh "scp /var/jenkins_home/workspace/version1/sample-app/target/sample.war ec2-user@3.91.0.47:/opt/tomcat/webapps/"
                }
            }
        }
    }

    post {

        success {
            echo "Successfully deployed ${APP_VERSION}"
        }

        failure {
            echo "Pipeline failed for ${APP_VERSION}"
        }
    }
}
