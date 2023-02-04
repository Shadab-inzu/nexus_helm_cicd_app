Pipeline{

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
                       sh 'mvn clearn package sonar:sonar'
                  }
                    
                }
            }
        }
    }
}