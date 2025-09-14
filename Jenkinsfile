pipeline {
    agent any
    environment {
        IMAGE_NAME = "arjukumar7/bookmyshow-app:v1"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature', url: 'https://github.com/arju7jha/Book-My-Show.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t %IMAGE_NAME% ./bookmyshow-app'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push %IMAGE_NAME%
                    """
                }
            }
        }
    }
}



// pipeline {
//     agent any
//     stages {
//         stage('Checkout') {
//             steps {
//                 git branch: 'feature', url: 'https://github.com/arju7jha/Book-My-Show.git'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 bat 'docker build -t arjukumar7/bookmyshow-app:local ./bookmyshow-app'
//             }
//         }
//         stage('Push to DockerHub') {
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
//                     bat '''
//                     echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
//                     docker push arjukumar7/bookmyshow-app:local
//                     '''
//                 }
//             }
//         }
//     }
// }

