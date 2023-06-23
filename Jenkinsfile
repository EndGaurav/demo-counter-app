pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/EndGaurav/demo-counter-app.git'
                }
            }
        }
        stage('Unit test') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Integration test') {
            steps {
                script {
                    sh 'mvn verify -DskipUnitTest'
                }
            }
        }
        stage('Building application') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }
    }
        
}