pipeline{
    agent any
    tools{
        nodejs 'nodejs20'
    }
    // environment {
    // HEROKU_CREDENTIALS = credentials('Heroku1')
    // }
    stages{
        stage('Clone repository'){
            steps{
                git 'https://github.com/WanjikuN/node-todo-cicd.git'
            }
        }
        stage('Install dependancies'){
            steps{
                sh 'npm install'
            }
        }
        // stage('Tests'){
        //     post{
        //         failure{
        //           mail bcc: '', body: 'Jenkins Test Failure', cc: '', from: '', replyTo: '', subject: 'Test Failed', to: 'cikunjoroge4@gmail.com'  
        //         }
        //     }
        //     steps{
        //         sh 'npm test'
        //     }
        // }

        stage('Deploy to Heroku'){
            steps{
               withCredentials([usernameColonPassword(credentialsId: 'Heroku1', variable: 'HEROKU_CREDENTIALS')]) {
                    sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/todo-nodejs.git master' } 
            }
        }
        stage('Slack Notifications'){
            steps{
                slackSend channel: '#trial', color: 'green', message: 'successful deployment of ${env.JOB_NAME}', teamDomain: 'wanjiku-workspace', tokenCredentialId: 'slack2' 
                 }
        }
    }
}