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
                    bat "echo ljcfyh_123@99| docker login --username 12112910@mail.sustech.edu.cn --password-stdin"
                    bat "docker tag teedy2024_manual maystern/teedy2024_manual"
                    bat "docker push maystern/teedy2024_manual"
            }
        }

       stage('Run containers') {
           steps {
               // Stop and remove containers if they are already running
               bat 'docker stop teedy_manual01 || true'
               bat 'docker rm teedy_manual01 || true'
               bat 'docker stop teedy_manual02 || true'
               bat 'docker rm teedy_manual02 || true'
               bat 'docker stop teedy_manual03 || true'
               bat 'docker rm teedy_manual03 || true'

               // Run new containers
               bat 'docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual'
               bat 'docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual'
               bat 'docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'
           }
       }
    }
}
