pipeline {
    agent any
        stage('Code Coverage') {
            steps {
                echo 'Running tests and generating Jacoco code coverage report...'
                sh 'mvn clean test jacoco:report'
            }
            post {
                always {
                    jacoco execPattern: '**/target/jacoco.exec',
                           classPattern: '**/target/classes',
                           sourcePattern: '**/src/main/java'
                }
            }
        }
    }
}
