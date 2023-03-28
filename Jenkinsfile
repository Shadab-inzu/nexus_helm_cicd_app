pipeline{
    agent any
    environment{
        VERSION= "${env.BUILD_ID}"
    }
    stages{

        stage('sonar quality status'){
            agent {

                docker {
                    image 'maven'
                }
            }

            steps{

                script{

                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }


                }
            }
        }

        stage('Quality gate status'){
            
            steps{

                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'  

                                       
                     }


                }
            }
            stage('docker build and push to nexus repo'){
                
                steps{

                    script{
                        
                        withCredentials([string(credentialsId: 'nexus_pass', variable: 'nexus_cred')]) {
                       sh '''
                       docker build -t 52.91.13.75:8083/springapp:${VERSION} .
                       docker login -u admin -p $nexus_cred 52.91.13.75:8083
                       docker push 52.91.13.75:8083/springapp:${VERSION}
                       docker rmi 52.91.13.75:8083/springapp:${VERSION}
                  }

                    }
                }
            }


        }
    }
