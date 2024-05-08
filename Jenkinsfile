pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Doc') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
            steps {
                bat 'mvn test --fail-never'
                bat 'mvn surefire-report:report'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/**/*.jar, **/target/**/*.war, **/target/surefire-reports/*.xml, **/target/pmd.xml', fingerprint: true
        }
    }
}
