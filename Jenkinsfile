def gitPullAll(String credentialsId) {
    sshagent([credentialsId]) {
        sh("git pull -all") 
    }
}

pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                gitPullAll "7981a5f7-164d-4c37-a12a-1a8f48ae3241"
                //sh label: '', script: 'git pull -all'
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
    }
}