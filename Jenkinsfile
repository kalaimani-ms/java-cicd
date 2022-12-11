pipeline{
    agent any 
        tools{
            maven 'MAVEN'
        }
        stages{
            stage ("maven_life_cycle"){
                script{
                    sh "mvn validate"
                    sh "mvn test"
            }
        }
    }
}
