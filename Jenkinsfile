pipeline {
    agent any

    stages {

        stage('nofity') {
            steps {
               slackSend channel: 'lms-project', color: '#439FE0', message: 'slackSend "started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"', teamDomain: 'devops-rkv5493', tokenCredentialId: 'slacksend'
            }
        }
        
        stage('Sonar Analysis') {
            steps {
                echo 'CODE QUALITY CHECK'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://3.98.148.249:9000" -e SONAR_TOKEN="sqp_0135bba75840ab307f31a1e480e7f211c25f8f37" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'CODE QUALITY DONE'
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
            }
        }

        stage('PostgreSQL deplyment & service') {
            steps {
                script {
                    echo 'apply PostgreSQL deplyment & service'
                    sh ('aws eks update-kubeconfig --name lms --region ca-central-1')
                    sh "kubectl get pods"
                    sh "cd api && kubectl apply -f database-secret.yml"
                    sh "cd api && kubectl apply -f database-deployment.yml"
                    sh "cd api && kubectl apply -f database-sevice.yml"
                    echo 'Database container is running'
                }
            }
        }

        stage('applying backend configMap ') {
            steps {
                script {
                    echo 'applying backend configMap'
                    sh "cd api && kubectl apply -f backend-configmap.yml"
                }
            }
        }
        stage('Build backend Docker Image') {
            steps {
                script {
                    echo 'Build backend Docker Image'
                    def version = sh(script: "cd api && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
                    sh "cd api && sudo docker build --build-arg VERSION=${version} -t ahmed12shire/lms-be ."
                    echo 'Image build complete'
                }
            }
        }


        stage('Push backend Docker Image') {
            steps {
                script {
                    // Push Docker image
                    sh "docker push ahmed12shire/lms-be"
                }
            }
        }

        stage('backend deplyment & service') {
            steps {
                script {
                    echo 'apply backend deplyment & service'
                    sh "cd api && kubectl apply -f backend-deployment.yml"
                    sh "cd api && kubectl apply -f backend-service.yml"
                    echo 'Database container is running'
                }
            }
        }

        stage('Build frontend Docker Image') {
            steps {
                script {
                    echo 'Build Docker Backend Image'
                    def version = sh(script: "cd webapp && cat package.json | grep '\"version\"' | cut -d '\"' -f 4", returnStdout: true).trim()
                    sh "cd webapp && docker build --build-arg VERSION=${version} -t ahmed12shire/lms-fe ."
                    echo 'Image build complete'
                }
            }
        }

        stage('Push frontend Docker Image') {
            steps {
                script {
                    // Push Docker image
                    sh "docker push ahmed12shire/lms-fe"
                }
            }
        }

        stage('frontend deplyment & service') {
            steps {
                script {
                    echo 'apply frontend deplyment & service'
                    sh "cd api && kubectl apply -f frontend-deployment.yml"
                    sh "cd api && kubectl apply -f frontend-service.yml"
                    echo 'frontend container is running'
                }
            }
        }
    }
}

