pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature', url: 'https://github.com/arju7jha/Book-My-Show.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t arjukumar7/bookmyshow-app:latest ./bookmyshow-app'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat '''
                    echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                    docker push arjukumar7/bookmyshow-app:latest
                    '''
                }
            }
        }
    }
}




// pipeline {
//   agent any

//   environment {
//     IMAGE_NAME = "arjukumar7/bookmyshow"   // <- change to your DockerHub repo
//     IMAGE_TAG  = "${env.BUILD_NUMBER}"
//   }

//   stages {
//     stage('Checkout') {
//       steps {
//         checkout scm
//       }
//     }

//     stage('Build Docker Image') {
//       steps {
//         sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
//         sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest"
//       }
//     }

//     stage('DockerHub Login & Push') {
//       steps {
//         withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'arjukumar7', passwordVariable: 'dckr_pat_SYwhwsghJLhj1RXvGvZNxab6l7Als')]) {
//           sh "echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin"
//           sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
//           sh "docker push ${IMAGE_NAME}:latest"
//         }
//       }
//     }

//     stage('Cleanup Local Images') {
//       steps {
//         // optional: free space on Jenkins agent
//         sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG} || true"
//       }
//     }
//   }

//   post {
//     success {
//       echo "Docker image pushed: ${IMAGE_NAME}:${IMAGE_TAG}"
//     }
//     failure {
//       echo "Pipeline failed."
//     }
//   }
// }
