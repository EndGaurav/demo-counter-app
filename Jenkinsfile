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
        stage('Static code analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonar-server') {
                            sh 'mvn clean package sonar:sonar'
                        }
                }
            }
        }
        stage('Quality gate checks') {
            steps {
               
                script { 
                    waitForQualityGate abortPipeline: false 
                    // timeout(time: 1, unit: 'HOURS') {
                    //     def qg = waitForQualityGate()
                    //     if (qg.status != 'OK') {
                    //         error "pipeline aborted due to quality gate failure: ${qg.status}"
                    //     }
                    //     else {
                    //         print "Pipeline successfully executed."
                    //     }
                    // }
                }
            }
        }
    }
        
}