pipeline {
    agent any
    stages {
            stage('Build') {
                steps {
                    sh 'mvn -B -D skipTests clean package'
                }
            }
    }
}
