pipeline {
    agent any

//     tools {
//         maven 'Maven' // Ensure Maven is set up in Jenkins' Global Tool Configuration with this name
//     }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    bat 'mvn clean compile'
                }
            }
        }

        stage('Generate Documentation') {
            steps {
                script {
                    // Generate Javadoc and package it into a JAR
                    bat 'mvn javadoc:jar'
                }
            }
        }

        stage('Run PMD') {
            steps {
                script {
                    // Run PMD analysis
                    bat 'mvn pmd:pmd'
                }
            }
        }

        stage('Test and Report') {
            steps {
                script {
                    // Run tests and generate Surefire reports
                    bat 'mvn test surefire-report:report'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive Javadocs, PMD reports, and Surefire reports
                archiveArtifacts artifacts: '**/target/site/apidocs/**, **/target/pmd.xml, **/target/surefire-reports/*.xml', fingerprint: true
            }
        }
    }

//     post {
//         always {
//             // Cleanup workspace after the build
//             cleanWs()
//         }
//         success {
//             echo 'Build was successful!'
//         }
//         failure {
//             echo 'Build failed!'
//         }
//     }
}
