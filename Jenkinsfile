pipeline{

    agent any

    stages{
        stage('Sonar quality status'){
            agent{
                docker{
                    image 'maven'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                // some block
                       sh 'mvn clean package sonar:sonar'
                  }
                    
                }
            }
        }
        stage('Quality gate status'){
            stepss{
                script{

                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
    }
}
