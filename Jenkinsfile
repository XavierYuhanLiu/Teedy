pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }
        stage('PMD'){
            steps {
                sh 'mvn clean install -U'
                sh 'mvn pmd:pmd'
            }
        }
        stage('Surfire'){
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        stage('Javadoc'){
            steps {
                sh 'mvn site --fail-never'
                sh 'mvn javadoc:javadoc --fail-never'
                sh 'mvn javadoc:jar --fail-never'
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