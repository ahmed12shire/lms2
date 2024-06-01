pipeline {
    agent any

    stages {
    //     stage('Sonar Analysis') {
    //         steps {
    //             echo 'CODE QUALITY CHECK'
    //             sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://3.96.171.159:9000" -e SONAR_TOKEN="sqp_15550378958d0e0e7ff45fbd03695ef1e832ec69" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
    //             echo 'CODE QUALITY DONE'
    //         }
    //     }

        stage('Docker Login') {
            steps {
                script {
                    // Docker login
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    }
                }
            }
        }

        stage('PostgreSQL deplyment & service') {
            steps {
                script {
                    echo 'apply PostgreSQL deplyment & service'
                    sh "cd api && kubectl apply -f database-secret.yml"
                    sh "kubectl apply -f database-deployment.yml"
                    sh "kubectl apply -f database-service.yml"
                    echo 'Database container is running'
                }
            }
        }

//         stage('Build backend Docker Image') {
//             steps {
//                 script {
//                     echo 'Build backend Docker Image'
//                     def version = sh(script: "cd api && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
//                     sh "cd api && docker build --build-arg VERSION=${version} -t ahmed12shire/lms-backend-j ."
//                     echo 'Image build complete'
//                 }
//             }
//         }

//         stage('Push backend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-backend-j"
//                 }
//             }
//         }

//         stage('Run backend Docker Container') {
//             steps {
//                 script {
//                     echo 'Running backend container'
//                     sh "docker run -d --name lms-backend-j -p 8080:8080 ahmed12shire/lms-backend-j"
//                     echo 'Backend container is running'
//                 }
//             }
//         }

//         stage('Build frontend Docker Image') {
//             steps {
//                 script {
//                     echo 'Build Docker Backend Image'
//                     def version = sh(script: "cd webapp && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
//                     sh "cd webapp && docker build --build-arg VERSION=${version} -t ahmed12shire/lms-frontend-j ."
//                     echo 'Image build complete'
//                 }
//             }
//         }

//         stage('Push frontend Docker Image') {
//             steps {
//                 script {
//                     // Push Docker image
//                     sh "docker push ahmed12shire/lms-frontend-j"
//                 }
//             }
//         }

//         stage('Run frontend Docker Container') {
//             steps {
//                 script {
//                     echo 'Running frontend container'
//                     sh "docker run -d --name lms-frontend-j -p 80:80 ahmed12shire/lms-frontend-j"
//                     echo 'Backend container is running'
//                 }
//             }
//         }
    }
}