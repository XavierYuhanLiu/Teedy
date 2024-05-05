pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn -B -DskipTests clean package'
                sh 'mvn pmd:pmd'
            }
        }
        stage('javadoc'){
            steps {
                sh 'mvn site --fail-never'
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