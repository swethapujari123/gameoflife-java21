
pipeline {
    agent none

    stages {

        stage('Checkout & Build') {
            agent { label 'master' }

            steps {
                git branch: 'main',
                    url: 'https://github.com/swethapujari123/gameoflife-java21.git'

                sh 'mvn clean package'

                stash includes: 'target/*.war', name: 'warfile'
            }
        }

        stage('Deploy') {
            agent { label 'jnlp-agent' }

            steps {
                unstash 'warfile'

                sh '''
                cp target/*.war /mnt/tomcat/webapps/gameoflife.war
                '''
            }
        }
    }
}
