pipeline {
    agent any
    stages {
        stage('Package') {
            steps {
                    checkout scmGit(branches: [[name: '*/master']], extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/Maystern/Teedy.git']])
                    bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Building image') {
            steps {
                // your command
                bat "docker build -t teedy2024_manual ."
            }
        }

        stage('Upload image') {
            steps {
                    bat "docker login"
                    bat "docker tag teedy2024_manual JiachengLuo/teedy2024_manual"
                    bat "docker push JiachengLuo/teedy2024_manual"
            }
        }

        stage('Run containers') {
            steps {
                bat 'docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual'
                bat 'docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual'
                bat 'docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'
            }
        }
    }
}
