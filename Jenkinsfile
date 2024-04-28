pipeline{
    agent any
    tools{
        maven 'local_maven'
    }

    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server'){
            steps{
                deploy adapters: [tomcat7(credentialsId: 'c862365e-9fd1-41d7-957b-c371fa3f55b2', path: '', url: 'http://192.168.0.123:8181/')],
                 contextPath: null, war: '**/*.war'
            }
        }
    }
}