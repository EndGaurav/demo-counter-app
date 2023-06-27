pipeline{
    
    agent any 

    parameters {
        choice(
            name: 'action',
            choices: 'create\ndestroy\nclusterDestroy',
            description: 'Create, update or delete your eks cluster' 
        )
        string(
            name: 'cluster',
            defaultValue: 'Master-Node-1',
            description: 'EKS cluster name'
        )
        string(
            name: 'regions',
            defaultValue: 'us-east-1',
            description: 'EKS cluster region'
        )
    }
    environment {
        ACCESS_KEY_ID = credentials('access_key')
        SECRET_ACCESS_KEY = credentials('secret_id')
    }
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/EndGaurav/demo-counter-app.git'
                }
            }
        }
        stage('Connect to EKS') {
            steps {
                script {
                    sh """
                        aws configure set aws_access_key_id = "$ACCESS_KEY_ID"
                        aws configure set aws_secret_access_key = "$SECRET_ACCESS_KEY"
                        aws configure set region = ""
                        aws eks --region ${params.region} update-kubeconfig --name ${params.cluster}
                    """
                }
            }
        }
        // stage('Deploy application to EKS cluster') {
        //     when { expression { params.action == 'create' } }

        //     steps {
        //         script {
        //             def apply = false
        //             try {
        //                 input message: 'Please confirm the apply to innitate the deployments', ok: 'Ready to apply the cofig'
        //                 apply = true
        //             }catch(err) {
        //                 apply = false
        //                 CurrentBuild = 'UNSTABLE'
        //             }

        //             if(apply) {
        //                 sh '''kubectl apply -f . '''
        //             }
        //         }
        //     }
        // }
        // --------------------------------------------------------------------------------------------------------------
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