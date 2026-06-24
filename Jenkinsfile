pipeline {
agent any

```
stages {

    stage('Checkout') {
        steps {
            git branch: 'master',
                url: 'https://github.com/swethapujari123/gameoflife-java21.git'
        }
    }

    stage('Build') {
        steps {
            sh 'mvn clean package'
        }
    }

    stage('Deploy to Slave') {
        steps {
            sshagent(['slave-ssh-key']) {
                sh '''
                scp target/*.war jenkins@172.31.86.119:/mnt/tomcat/webapps/gameoflife.war
                '''
            }
        }
    }
}

post {
    success {
        echo 'Deployment Successful'
    }
}
