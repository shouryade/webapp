pipeline {
    agent {
        label 'master || built-in'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Sonar-Report') {
            steps {
                script {
                    env.SONAR_TOKEN = '0f4710bc83ed3dcde89fd96948660417042b1479'
                    sh 'echo $SONAR_TOKEN'
                    sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=shouryade_webapp'
                }
            }
        }
    }
}
