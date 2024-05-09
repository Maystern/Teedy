pipeline {
    agent any
    stages{
        stage('Package') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/Maystern/Teedy']])
                bat 'mvn -B -DskipTests clean package'
        }
    }
    stage('Building image') {
        steps{
            //your command

        }
    }

    stage('Upload image') {
        steps{
            //your command
        }
    }

    stage('Run containers'){
        steps{
            //your command
        }
    }
}
