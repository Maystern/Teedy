pipeline {
    agent any
    stages {
        stage('Package') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        } // 这里缺少了一个闭合的大括号

        stage('Building image') {
            steps {
                // your command
                bat "docker build -t teedy2024_manual ."
            }
        }

        stage('Upload image') {
            steps {
                // your command
                cho 'No upload commands specified'
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
