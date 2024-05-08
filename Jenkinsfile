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
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.ear', fingerprint: true
        }
    }
//
// //     tools {
// //         maven 'Maven' // Ensure Maven is set up in Jenkins' Global Tool Configuration with this name
// //     }
//
//     stages {
//         stage('Checkout SCM') {
//             steps {
//                 checkout scm
//             }
//         }
//
//         stage('Build') {
//             steps {
//                 script {
//                     bat 'mvn clean compile'
//                 }
//             }
//         }
//
//         stage('Generate Documentation') {
//             steps {
//                 script {
//                     // Generate Javadoc and package it into a JAR
//                     bat 'mvn test --fail-never'
//                     bat 'mvn javadoc:jar'
//                 }
//             }
//         }
//
//         stage('Run PMD') {
//             steps {
//                 script {
//                     // Run PMD analysis
//                     bat 'mvn pmd:pmd'
//                 }
//             }
//         }
//
//         stage('Test and Report') {
//             steps {
//                 script {
//                     // Run tests and generate Surefire reports
//                     bat 'mvn test surefire-report:report'
//                 }
//             }
//         }
//
//         stage('Archive Artifacts') {
//             steps {
//                 // Archive Javadocs, PMD reports, and Surefire reports
//                 archiveArtifacts artifacts: '**/target/site/apidocs/**, **/target/pmd.xml, **/target/surefire-reports/*.xml', fingerprint: true
//             }
//         }
//     }

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
