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
                    waitForQualityGate abortPipeline: true, credentialsId: 'sonar-token' 
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
        stage('Upload artifact to nexus') {
            steps {
                // for making dynamic nature of jenkins to fetch there is plugin called: pipeline utility steps.
                // search for how to read file using pipeline utility steps.
                script {
                    def readArtifactVersion = readMavenPom file: 'pom.xml'  
                    def nexusRepo = readArtifactVersion.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-release"
                    // def pomVersion = readArtifactVersion.version
                    nexusArtifactUploader artifacts: [
                            [
                                artifactId: 'springboot',
                                classifier: '', 
                                file: 'target/Uber.jar', 
                                type: 'jar'

                            ]
                        ],
                        credentialsId: 'nexus-cred',
                        groupId: 'com.example', 
                        nexusUrl: '35.173.191.138:8081',
                        nexusVersion: 'nexus3', 
                        protocol: 'http',
                        repository: "${nexusRepo}",
                        version: "${readArtifactVersion.version}"
                }
            }
        }
    }
        
}