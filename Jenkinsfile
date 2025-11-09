pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata: 
  labels:
    app: jenkins-kaniko
spec:
  serviceAccountName: jenkins
  containers:
    - name: kaniko
      image: gcr.io/kaniko-project/executor:debug-v0.19.0
      command:
        - /busybox/cat
      tty: true
      volumeMounts:
        - name: kaniko-secret
          mountPath: /kaniko/.docker/
  volumes:
    - name: kaniko-secret
      secret:
        secretName: dockerhub-credentials
"""
        }
    }
    
    environment {
        IMAGE_NAME = 'docker.io/jacob14meju/flask-aws-monitor'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Jacob14meju/kubernetes-deployment.git'
            }
        }
        
        stage('Parallel Checks') {
           parallel{
                stage('Linting') {
                    steps {
                        echo 'linting steps for Python, Shell, and Dockerfile'
                    }
                }
                stage('Security Scan') {
                    steps {
                        echo 'security scanning steps for dependencies and container security'
                    }
                }
           }
            
        }
        
        stage('Build Docker Image and push  to docker hub') {
            steps {
                container('kaniko') {
                    sh """
                        /kaniko/executor \
                        --context $(pwd)/docker \
                        --dockerfile $(pwd)/docker/Dockerfile \
                        --destination ${IMAGE_NAME}:${env.BUILD_NUMBER} \
                        --destination ${IMAGE_NAME}:latest \
                        --cache=true
                    """
                }
            }
        }

        stage('push changes to github'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-cred', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh """
                        git config user.email "mejuboygamer@gmail.com"
                        git config user.name "${GIT_USERNAME}"
                        sed -i "s/tag:.*/tag: ${env.BUILD_NUMBER}/" flask-monitor/values.yaml
                        git add .
                        git commit -m "Automated commit from Jenkins Pipeline - Build #${env.BUILD_NUMBER}"
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Jacob14meju/kubernetes-deployment.git main
                    """
            }
        }
    }
        
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check logs for details.'
        }
    }
}

