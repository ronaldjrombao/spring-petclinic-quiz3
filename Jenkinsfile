pipeline {
    agent any

    tools {
        maven "M3"
    }

    environment {
        GIT_REPO = 'git@github.com:ronaldjrombao/spring-petclinic-quiz3.git'  // Use SSH URL
        BRANCH = 'master'
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository using SSH...'
                git branch: "${BRANCH}", url: "${GIT_REPO}", credentialsId: 'Comp367-SSH'
            }
        }

        stage('Code Coverage') {
            steps {
                echo 'Running tests and generating Jacoco code coverage report...'
                // Run tests and generate the Jacoco report
                sh 'mvn clean test jacoco:report'
            }

            post {
                always {
                    // Publish the Jacoco report. Adjust patterns if needed.
                    jacoco execPattern: '**/target/jacoco.exec',
                           classPattern: '**/target/classes',
                           sourcePattern: '**/src/main/java'
                }
            }
        }
    }
}
