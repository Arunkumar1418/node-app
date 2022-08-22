pipeline {
    agent any
    stages {
        stage('checkout from SCM') {
            steps {
                git 'https://github.com/Arunkumar1418/node-app.git'
            }
        }
        stage('scan') {
            steps {
                sh "docker run -v ${WORKSPACE}:/src --workdir /src returntocorp/semgrep-agent:v1 semgrep-agent --config p/ci --config p/security-audit --config p/secrets"
            }
        }
        stage('sonarscan'){
            steps {
                withSonarQubeEnv('soanrqube'){ // You can override the credential to be used
                sh 'mvn sonar:sonar'
                }
            }
        }    
        
    }
}