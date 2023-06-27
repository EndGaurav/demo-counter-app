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
        // stage('Unit test') {
        //     steps {
        //         script {
        //             sh 'mvn test'
        //         }
        //     }
        // }
        // stage('Integration test') {
        //     steps {
        //         script {
        //             sh 'mvn verify -DskipUnitTest'
        //         }
        //     }
        // }
        // stage('Building application') {
        //     steps {
        //         script {
        //             sh 'mvn clean install'
        //         }
        //     }
        // }
        // stage('Static code analysis') {
        //     steps {
        //         script {
        //             withSonarQubeEnv('sonar-server') {
        //                     sh 'mvn clean package sonar:sonar'
        //                 }
        //         }
        //     }
        // }
        // stage('Quality gate checks') {
        //     steps {
               
        //         script { 
        //             waitForQualityGate abortPipeline: true, credentialsId: 'sonar-token' 
        //             // timeout(time: 1, unit: 'HOURS') {
        //             //     def qg = waitForQualityGate()
        //             //     if (qg.status != 'OK') {
        //             //         error "pipeline aborted due to quality gate failure: ${qg.status}"
        //             //     }
        //             //     else {
        //             //         print "Pipeline successfully executed."
        //             //     }
        //             // }
        //         }
        //     }
        // }
        // stage('Upload artifact to nexus') {
        //     steps {
        //         // for making dynamic nature of jenkins to fetch there is plugin called: pipeline utility steps.
        //         // search for how to read file using pipeline utility steps.
        //         script {
        //             def readArtifactVersion = readMavenPom file: 'pom.xml'  
        //             def nexusRepo = readArtifactVersion.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-release"
        //             // def pomVersion = readArtifactVersion.version
        //             nexusArtifactUploader artifacts: [
        //                     [
        //                         artifactId: 'springboot',
        //                         classifier: '', 
        //                         file: 'target/Uber.jar', 
        //                         type: 'jar'

        //                     ]
        //                 ],
        //                 credentialsId: 'nexus-cred',
        //                 groupId: 'com.example', 
        //                 nexusUrl: '100.24.60.89:8081',  // replace it as per node ip.
        //                 nexusVersion: 'nexus3', 
        //                 protocol: 'http',
        //                 repository: "${nexusRepo}",
        //                 version: "${readArtifactVersion.version}"
        //                 // version: '2.0.1-SNAPSHOT'
        //         }
        //     }
        // }
        // stage('Docker image build') {
        //     steps {
        //         script {
        //             sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
        //             sh 'docker image tag $JOB_NAME:v1.$BUILD_ID endgaurav/$JOB_NAME:V1.$BUILD_ID'
        //             sh 'docker image tag $JOB_NAME:v1.$BUILD_ID endgaurav/$JOB_NAME:latest'

        //         }
        //     }
        // }
        // stage('Pushing image to docker hub') {
        //     steps {
        //         script {
        //             withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'dockerPasswd', usernameVariable: 'dockerUsername')]) {
        //                     sh "docker login -u ${dockerUsername} -p ${dockerPasswd}"
        //                     sh 'docker image push endgaurav/$JOB_NAME:V1.$BUILD_ID'
        //                     sh 'docker image push endgaurav/$JOB_NAME:latest'
                   
        //                     sh 'docker image rm $JOB_NAME:v1.$BUILD_ID endgaurav/$JOB_NAME:V1.$BUILD_ID endgaurav/$JOB_NAME:latest'
        //             }
        //         }
        //     }
        // }
    }
        
}