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
                            script{
                                sh 'mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=maven-project \
                                    -Dsonar.host.url=http://3.108.238.160:9000 \
                                    -Dsonar.login=sqp_25b27fc8dc5db466aa19d99a0407148bc187c8c3'
                            }
                        }
            }
        }
    }