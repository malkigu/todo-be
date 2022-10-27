pipeline {
    agent any

    environment {
        DOCKER_USERNAME = credentials('jenkins-user-for-artifact-repository')
        DOCKER_PASSWORD = credentials('jenkins-user-for-artifact-repository')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t malkigu/todo-be:latest --target builder .'
            }
        }
        stage('Delivery') {
            steps {
                echo 'Delivery....'
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t malkigu/todo-be:latest --target delivery .'
            }
        }
         stage('Cleanup') {
            steps {
                echo 'Cleanup....'
                sh 'docker system prune -f'
            }
        }
         stage('Push') {
            steps {
                echo 'pushing to dockerhub....'
                sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                sh 'docker push malkigu/todo-be:latest'
            }
        }
    }
}
