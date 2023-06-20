pipeline{
    agent any
    tools{
        nodejs 'nodejs20'
    }
    environment {
    HEROKU_CREDENTIALS = credentials('Heroku1')
    }
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
               withCredentials([usernamePassword(credentialsId: 'Heroku1', usernameVariable: 'HEROKU_USERNAME', passwordVariable: 'HEROKU_PASSWORD')]) {
                 sh 'heroku login --username $HEROKU_USERNAME --password $HEROKU_PASSWORD'
                 sh 'git push https://git.heroku.com/todo-nodejs.git master'
                } 
            }
        }
        stage('Slack Notifications'){
            steps{
                slackSend channel: '#ip1-devops', color: '#008000', message: "Successful deployment of ${env.JOB_NAME} ,Build number ${env.BUILD_NUMBER} .  (<https://gallerypat.herokuapp.com/|Gallery url>)", teamDomain: 'patriciaip1', tokenCredentialId: 'slackIP'
            }
        }
    }
}