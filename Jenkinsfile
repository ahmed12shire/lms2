pipeline {
    agent any

    stages {
       stage('nofity') {
            steps {
                slackSend channel: 'eks', color: '#439FE0', message: 'slackSend "production going to start"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }
    
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'sudo docker run --rm -e SONAR_HOST_URL="http://15.222.239.12/:9000" -e SONAR_TOKEN="sqp_1cdd446e0fc471a2c8e8ed8fb9138801896aaa72" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'CODE QUALITY DONE'
                slackSend channel: 'eks', color: '#439FE0', message: 'Sonar Analysis completed', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    // Docker login
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    }
                }
                slackSend channel: 'eks', color: '#439FE0', message: 'dockerhub login success', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }
        stage('Approval') {
            steps {
                 script{
                timeout(time: 5,unit: "MINUTES"){
                slackSend channel: ' team-updates', message: "slackSend 'started ${env.JOB_NAME}  (http://15.222.239.12:8080/job/lms-eks/${env.BUILD_NUMBER}/)'", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
                input message:'Approve to Deploy',ok: 'Yes'
            }
        }
    }
}
        stage('nofity after approval') {
            steps {
               slackSend channel: 'eks', color: '#439FE0', message: 'slackSend "started LMS production"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }

        
        // stage('PostgreSQL deplyment & service') {
        //     steps {
        //         script {
        //             echo 'apply PostgreSQL deplyment & service'
        //             sh ('aws eks update-kubeconfig --name lms --region ca-central-1')
        //             sh "kubectl get pods"
        //             sh "cd api && kubectl apply -f database-secret.yml"
        //             sh "cd api && kubectl apply -f database-deployment.yml"
        //             sh "cd api && kubectl apply -f database-sevice.yml"
        //             echo 'Database container is running'
        //         }
        //     }
        // }

        // stage('applying backend configMap ') {
        //     steps {
        //         script {
        //             echo 'applying backend configMap'
        //             sh "cd api && kubectl apply -f backend-configmap.yml"
        //         }
        //     }
        // }
        // stage('Build backend Docker Image') {
        //     steps {
        //         script {
        //             echo 'Build backend Docker Image'
        //             def version = "1.0.${BUILD_NUMBER}" 
                    
        //             // Building and tagging the Docker image with the version number
        //             sh "cd api && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-be:${version} ."
        //             echo "Image build complete. Tagged as: ahmed12shire/lms-be:${version}"
        //         }
        //     }
        // } 


        // stage('Push backend Docker Image') {
        //     steps {
        //         script {
        //             // Push Docker image
        //             sh "docker push ahmed12shire/lms-be:${version}"
        //         }
        //     }
        // }

        // stage('backend deplyment & service') {
        //     steps {
        //         script {
        //             echo 'apply backend deplyment & service'
        //             sh "cd api && kubectl apply -f backend-deployment.yml"
        //             sh "cd api && kubectl apply -f backend-service.yml"
        //             echo 'Database container is running'
        //         }
        //     }
        // }

        // stage('Build frontend Docker Image') {
        //     steps {
        //         script {
        //             echo 'Build frontend Docker Image'
        //             def version = "1.0.${BUILD_NUMBER}" 
                    
        //             // Building and tagging the Docker image with the version number
        //             sh "cd webapp && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-fe:${version} ."
        //             echo "Image build complete. Tagged as: ahmed12shire/lms-fe:${version}"
        //         }
        //     }
        // }

        // stage('Push frontend Docker Image') {
        //     steps {
        //         script {
        //             // Push Docker image
        //             sh "docker push ahmed12shire/lms-fe:${version}"
        //         }
        //     }
        // }

        // stage('frontend deplyment & service') {
        //     steps {
        //         script {
        //             echo 'apply frontend deplyment & service'
        //             sh "cd api && kubectl apply -f frontend-deployment.yml"
        //             sh "cd api && kubectl apply -f frontend-service.yml"
        //             echo 'frontend container is running'
        //         }
        //     }
        // }
        
    }
        post {
        failure {
            slackSend channel: 'eks', color: '#FF0000', message: "Pipeline failed: ${env.stage} - ${currentBuild.fullDisplayName}", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
        }
        success {
            slackSend channel: 'eks', color: '#00FF00', message: "Pipeline succeeded: ${env.stage} - ${currentBuild.fullDisplayName}", teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
        }
    }
}
