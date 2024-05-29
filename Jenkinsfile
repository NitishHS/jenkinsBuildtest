pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/NitishHS/jenkinsBuildtest.git'
            }
        }
        
        stage('Build') {
            steps {
                bat "${MAVEN_HOME}\\bin\\mvn clean install sonar:sonar"
                //sh "${MAVEN_HOME}/bin/mvn clean install sonar:sonar"
            }
        }
        
        stage('Test') {
            steps {
                // Run the Maven tests
                bat "${MAVEN_HOME}\\bin\\mvn test"
                //sh "${MAVEN_HOME}/bin/mvn test"
            }
            post {
                always {
                    junit '/target/surefire-reports/a.xml'
                }
            }
        }

        stage('Package') {
            steps {
                bat "${MAVEN_HOME}\\bin\\mvn package"
                //sh "${MAVEN_HOME}/bin/mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
