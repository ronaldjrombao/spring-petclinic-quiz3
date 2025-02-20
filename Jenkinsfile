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

        stage('Generate Coverage') {
            steps {
                echo 'Running tests and generating JaCoCo report...'
                sh 'mvn clean test jacoco:report'
            }
            post {
                always {
                    script {
                        step([
                            $class: 'JacocoPublisher',
                            execPattern: '**/target/jacoco.exec',
                            classPattern: '**/target/classes',
                            sourcePattern: '**/src/main/java',
                            changeBuildStatus: true
                        ])
                    }
                }
            }
        }
    }
}
