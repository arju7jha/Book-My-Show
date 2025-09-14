pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://52.53.163.10:9000'  // Replace with your SonarQube server IP
        SONAR_TOKEN = credentials('sqp_5e15d2fcddc58c50caa7a8637d92569cbc06818e')       // Add your SonarQube token in Jenkins credentials
    }

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/arju7jha/Book-My-Show.git'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                script {
                    sh """
                    docker run --rm \
                        -e SONAR_HOST_URL=${SONAR_HOST_URL} \
                        -e SONAR_LOGIN=${SONAR_TOKEN} \
                        -v $WORKSPACE:/usr/src sonarsource/sonar-scanner-cli
                    """
                }
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred') {
                        sh 'docker build -t bookmyshow:v1 .'
                        sh 'docker tag bookmyshow:v1 arjukumar7/bookmyshow:v1'
                        sh 'docker push arjukumar7/bookmyshow:v1'
                    }
                }
            }
        }

        stage('Deploy to Container') {
            steps {
                sh 'docker run -d --name bookmyshow-app -p 3130:3000 arjukumar7/bookmyshow:v1'
            }
        }
        
        // stage('Deploy to Kubernetes') {
        //     steps {
        //         script {
        //             withKubeConfig(credentialsId: 'k8s-config', namespace: 'akshat-ns') {
        //                 sh 'kubectl apply -f deployment.yml'
        //                 sh 'kubectl apply -f service.yml'
        //                 sh 'kubectl apply -f usernode-js-service.yml'
        //                 sh 'kubectl apply -f userprofile-deployment.yml'
        //             }
        //         }
        //     }
        // }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs!'
        }
    }
}








// pipeline {
//     agent any
//     environment {
//         IMAGE_NAME = "arjukumar7/bookmyshow-app:v1"
//     }
//     stages {
//         stage('Checkout') {
//             steps {
//                 git branch: 'feature', url: 'https://github.com/arju7jha/Book-My-Show.git'
//             }
//         }
//         stage('Build Docker Image') {
//             steps {
//                 bat 'docker build --no-cache -t %IMAGE_NAME% ./bookmyshow-app'
//             }
//         }
//         stage('Push to DockerHub') {
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
//                     bat """
//                     docker login -u %DOCKER_USER% -p %DOCKER_PASS%
//                     docker push %IMAGE_NAME%
//                     """
//                 }
//             }
//         }
//     }
// }
