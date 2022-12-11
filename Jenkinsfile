pipeline{
    agent any 
        tools{
            maven 'MAVEN'
        }
        stages{
            stage ("maven_life_cycle"){
                steps{
                    script{
                        sh "mvn validate"
                        sh "mvn test"
                        sh "mvn compile"
                        sh "mvn verify"
                        sh "mvn install"
                        }
                }
            }
            stage("sonarqube_analysis"){        
                        steps{
                            script{withSonarQubeEnv(credentialsId: 'sonar-id'){
                                sh 'mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=javaapp \
                                    -Dsonar.host.url=http://3.108.236.31:9000 \
                                    -Dsonar.login=sqp_0b6ff490957ba48b628928630d714f1a3d97cefb'
                            }
                        }
                    }
            }

            stage("quality gate pass"){
                steps{
                    script{withSonarQubeEnv(credentialsId: 'sonar-id'){
                        waitForQualityGate abortPipeline: true, credentialsId: 'sonar-id'

                        
                    }
                }
            }
        }
    }
}