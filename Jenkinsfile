pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-pat',
                    url: 'https://github.com/deepanchakravarthykiaq-ctrl/sonarqube-demo.git'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=devops-sonarqube-demo \
                          -Dsonar.projectName=devops-sonarqube-demo \
                          -Dsonar.sources=.
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build and SonarQube scan completed successfully!'
        }
        failure {
            echo 'Build failed. Check the Jenkins Console Output.'
        }
    }
}
