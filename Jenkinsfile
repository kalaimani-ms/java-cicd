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
                        def mvn = tool 'Default Maven';
                        withSonarQubeEnv() {
                        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=java"
            }
        }
    }
}