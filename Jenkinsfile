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
                                sh 'mvn clean verify sonar:sonar'      
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