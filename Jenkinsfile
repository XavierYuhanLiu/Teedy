pipeline {
    agent any
    stages{
        stage('Package'){
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Build Docket'){
            steps {
                sh 'docker build -t teedy .'
            }
        }
        stage('Upload DockerHub') {
            steps {
                sh 'docker tag teedy xavieryuhanliu/teedy'
                sh 'docker push xavieryuhanliu/teedy'
            }
        }
        stage('Run') {
            steps {
                sh 'docker run -d -p 8082:8080 teedy'
                sh 'docker run -d -p 8083:8080 teedy'
                sh 'docker run -d -p 8084:8080 teedy'
            }
        }

    }

    post {
        always{
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}