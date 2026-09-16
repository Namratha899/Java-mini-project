```groovy
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

        stage('Checkout') {
            steps {
                git(
                    branch: "${APP_VERSION}",
                    url: 'https://github.com/Namratha899/Java-mini-project.git'
                )
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

                    sh "scp target/sample-1.0.0.war ec2-user@3.91.0.47:/opt/tomcat/webapps/"
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
```
