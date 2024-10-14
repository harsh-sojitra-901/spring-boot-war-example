pipeline {
    agent any
     tools {
        maven 'maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                bat "mvn test"
               // slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                bat "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: '466b6521-061c-4b25-97be-3b47aaa0338f', path: '', url: 'http://13.127.241.151:8081')], contextPath: '/app', war: '**/*.war'              
            }
            
        }
        stage("Deploy on Prod"){
            //  input {
            //     message "Should we continue?"
            //     ok "Yes we Should"
            // }
            
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: '466b6521-061c-4b25-97be-3b47aaa0338f', path: '', url: 'http://13.127.241.151:8081')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
             //slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
             //slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
    }
}
