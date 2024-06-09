pipeline {
    agent any

    stages {
//        stage('nofity') {
//             steps {
//                 slackSend channel: 'eks', color: '#439FE0', message: 'slackSend "production going to start"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }
    
//         stage('Sonar Analysis') {
//             steps {
//                 echo 'CODE QUALITY CHECK'
//                 sh 'sudo docker run --rm -e SONAR_HOST_URL="http://3.96.170.219:9000" -e SONAR_TOKEN="sqp_40decc8be7549a419301a10af4ec6f924f3a36d9" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
//                 echo 'CODE QUALITY DONE'
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Sonar Analysis completed', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

//         stage('Docker Login') {
//             steps {
//                 script {
//                     // Docker login
//                     withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
//                         sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
//                     }
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'dockerhub login success', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }
//         stage('Approval') {
//             steps {
//                  script{
//                 timeout(time: 5,unit: "MINUTES"){
//                 slackSend channel: ' team-updates', message: "slackSend 'started ${env.JOB_NAME}  (http://3.96.170.219:8080/job/lms-eks/${env.BUILD_NUMBER}/)'", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//                 input message:'Approve to Deploy',ok: 'Yes'
//             }
//         }
//             slackSend channel: 'eks', color: '#439FE0', message: 'request to build approved', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//     }
// }
//         stage('nofity after approval') {
//             steps {
//                slackSend channel: 'eks', color: '#439FE0', message: 'slackSend "started LMS production"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

        
//         stage('PostgreSQL deplyment & service') {
//             steps {
//                 script {
//                     echo 'apply PostgreSQL deplyment & service'
//                     sh "kubectl get pods"
//                     sh "cd api && kubectl apply -f database-secret.yml"
//                     sh "cd api && kubectl apply -f database-deployment.yml"
//                     sh "cd api && kubectl apply -f database-sevice.yml"
//                     echo 'Database container is running'
//                 }
//                slackSend channel: 'eks', color: '#439FE0', message: 'PostgreSQL deplyment & service complete', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend' 
//             }
//         }

//         stage('applying backend configMap ') {
//             steps {
//                 script {
//                     echo 'applying backend configMap'
//                     sh "cd api && kubectl apply -f backend-configmap.yml"
//                 }
//             }
//         }
//         stage('Build backend Docker Image') {
//             steps {
//                 script {
//                     echo 'Build backend Docker Image'
//                     def version = "${BUILD_NUMBER}" 
                    
//                     // Building and tagging the Docker image with the version number
//                     sh "cd api && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-be:${version} ."
//                     echo "Image build complete. Tagged as: ahmed12shire/lms-be:${version}"
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Backend docker build complete', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         } 


//         stage('Push backend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-be"
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Backened imager pushed', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

//         stage('backend deplyment & service') {
//             steps {
//                 script {
//                     echo 'apply backend deplyment & service'
//                     sh "cd api && kubectl apply -f backend-deployment.yml"
//                     sh "cd api && kubectl apply -f backend-service.yml"
//                     echo 'Backend container is running'
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Backend deplyment & service complete', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

//         stage('Build frontend Docker Image') {
//             steps {
//                 script {
//                     echo 'Build frontend Docker Image'
//                     def version = "${BUILD_NUMBER}" 
                    
//                     // Building and tagging the Docker image with the version number
//                     sh "cd webapp && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-fe:${version} ."
//                     echo "Image build complete. Tagged as: ahmed12shire/lms-fe:${version}"
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Frontend docker build complete', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

//         stage('Push frontend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-fe"
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Frontend imager pushed', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

//         stage('frontend deplyment & service') {
//             steps {
//                 script {
//                     echo 'apply frontend deplyment & service'
//                     sh "cd api && kubectl apply -f frontend-deployment.yml"
//                     sh "cd api && kubectl apply -f frontend-service.yml"
//                     echo 'frontend container is running'
//                 }
//                 slackSend channel: 'eks', color: '#439FE0', message: 'Frontend deplyment & service complete', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
//             }
//         }

        stage('log file') {
            steps {
                slackSend channel: 'eks', color: '#439FE0', message: "Build Log: ${env.BUILD_URL}console", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }
        
    }
    //     post {
    //     failure {
    //         slackSend channel: 'eks', color: 'green', message: "Pipeline failed: ${currentBuild.fullDisplayName} - ${env.STAGE_NAME}", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
    //     }
    //     success {
    //         slackSend channel: 'eks', color: 'red', message: "Pipeline succeeded: ${currentBuild.fullDisplayName} - ${env.STAGE_NAME}", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
    //     }
        post {
        always {
            script {
                def consoleOutput = ""
                // Construct console text URL
                def consoleUrl = "${env.BUILD_URL}consoleText"
                try {
                    // Get console output
                    def logFile = sh(script: "curl -s ${consoleUrl}", returnStdout: true)
                    // Truncate the log if it's too long to avoid Slack message size limits
                    if (logFile.size() > 100000) {
                        consoleOutput = logFile.readLines().takeRight(500).join('\n')
                        consoleOutput += "\n...(truncated)"
                    } else {
                        consoleOutput = logFile
                    }
                    // Send console output to Slack
                    slackSend(
                        color: '#439FE0',
                        message: "Build Console Output:\n```${consoleOutput}```",
                    channel: 'eks',
                    teamDomain: 'devops-rkv5493',
                    tokenCredentialId: 'slacksend'
                )
                     
            }       catch (Exception e) {
                    println("Failed to read console output: ${e.message}")
                }
        }
    }
}
}