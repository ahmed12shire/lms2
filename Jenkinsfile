pipeline {
    agent any

    stages {

        stage('nofity') {
            steps {
               slackSend channel: 'lms-project', color: '#439FE0', message: 'slackSend "started LMS production"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }
        
        // stage('Sonar Analysis') {
        //     steps {
        //         echo 'CODE QUALITY CHECK'
        //         sh 'sudo docker run --rm -e SONAR_HOST_URL="http://3.99.221.240:9000" -e SONAR_TOKEN="sqp_3adee885ad8ed219b3a22db7bcd6320c362d1008" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
        //         echo 'CODE QUALITY DONE'
        //     }
        // }

        // stage('Docker Login') {
        //     steps {
        //         script {
        //             // Docker login
        //             withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
        //                 sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
        //             }
        //         }
        //     }
        // }
        stage('Deploy approval request') {
             steps {
                script {
            // Send message to Slack for approval
            def approvalMessage = "Deployment approval needed from Ahmed Shire. Please approve or reject this deployment in Slack."
            def approvalResponse = slackSend(channel: 'lms-project', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend', message: approvalMessage)

            // Wait for approval
            def isApproved = waitForApproval(approvalResponse)

            if (isApproved) {
                echo "Deployment approved. Proceeding to the next stage."
                // Proceed to the next stage
                // Insert your deployment steps here
            } else {
                error "Deployment rejected. Aborting deployment process."
            }
        }
    }
}

            def waitForApproval(approvalResponse) {
            // Assuming approvalResponse contains the text received from Slack
            if (approvalResponse.contains("approved")) {
            return true
            } else {
            return false
    }
}

//         stage('PostgreSQL deplyment & service') {
//             steps {
//                 script {
//                     echo 'apply PostgreSQL deplyment & service'
//                     sh ('aws eks update-kubeconfig --name lms --region ca-central-1')
//                     sh "kubectl get pods"
//                     sh "cd api && kubectl apply -f database-secret.yml"
//                     sh "cd api && kubectl apply -f database-deployment.yml"
//                     sh "cd api && kubectl apply -f database-sevice.yml"
//                     echo 'Database container is running'
//                 }
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
//                     def version = sh(script: "cd api && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
//                     sh "cd api && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-be ."
//                     echo 'Image build complete'
//                 }
//             }
//         }


//         stage('Push backend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-be"
//                 }
//             }
//         }

//         stage('backend deplyment & service') {
//             steps {
//                 script {
//                     echo 'apply backend deplyment & service'
//                     sh "cd api && kubectl apply -f backend-deployment.yml"
//                     sh "cd api && kubectl apply -f backend-service.yml"
//                     echo 'Database container is running'
//                 }
//             }
//         }

//         stage('Build frontend Docker Image') {
//             steps {
//                 script {
//                     echo 'Build Docker Backend Image'
//                     def version = sh(script: "cd webapp && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
//                     sh "cd webapp && docker build --build-arg VERSION=${version} -t ahmed12shire/lms-fe ."
//                     echo 'Image build complete'
//                 }
//             }
//         }

//         stage('Push frontend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-fe"
//                 }
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
//             }
//         }
    }
}

