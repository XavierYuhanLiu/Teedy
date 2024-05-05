pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('InstallAndTest'){
            steps {
                sh 'mvn clean install -U'
                sh 'mvn test'
            }
        }
        stage('PMDandJavadocandSurefire'){
            steps {
                sh 'mvn pmd:pmd'
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