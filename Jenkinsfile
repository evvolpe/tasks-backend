pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
        stage ('Unite Tests') {
            steps {
                sh "mvn test"
            }
        }
    }
}