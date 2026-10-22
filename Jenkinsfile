pipeline {
agent any

stages {
    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/deepanchakravarthy1qg-ctrl/sonarqube-demo.git'
        }
    }

    stage('SonarQube Scan') {
        steps {
            script {
                def scannerHome = tool 'sonarScanner'

                withSonarQubeEnv('SonarQube') {
                    sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=devops-sonarqube-demo \
                        -Dsonar.projectName=devops-sonarqube-demo \
                        -Dsonar.sources=.
                    """
                }
            }
        }
    }
}

post {
    success {
        echo 'SonarQube analysis completed successfully!'
    }
    failure {
        echo 'Build failed. Check the Jenkins Console Output.'
    }
}

}
