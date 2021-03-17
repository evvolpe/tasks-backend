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
        stage ('Sonar Analisys') {
           environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh "${scannerHome}/var/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=09f38b64beb812a207992386921bf0646cdfb3b3 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
        stage ('Quality Gate') {
            steps {
                sleep(30)
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}