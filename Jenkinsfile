pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven/bin"
    }
    stages{
        stage("Git Checlout"){
            steps{
                git 'https://github.com/krangaswamy1234/javaloginapp.git'
            }
        }
        stage("Code Build"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("SonarQube Analysis"){
            steps{
                withSonarQubeEnv('SonarQube-Server-8.9.2'){
                    sh 'mvn sonar:sonar'
                }
            }

        }
        stage("Quality Gate"){
            steps{
                timeout(unit: 'SECONDS', time: 300){
                    waitForQualityGate abortPipeline: true
                }
                
            }
        }
    }
    
}
