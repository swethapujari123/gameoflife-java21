
pipeline {
agent any


stages {

    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/swethapujari123/gameoflife-java21.git'
        }
    }

    stage('Build') {
        steps {
            sh 'mvn clean package'
            sh 'ls -ltr target/'
        }
    }

    stage('Deploy') {
        steps {
            sh '''
            scp -o StrictHostKeyChecking=no \
            target/*.war \
            root@172.31.86.119:/mnt/apache-tomcat-10.1.56/webapps/gameoflife.war
            '''
        }
    }
}

post {
    success {
        echo 'WAR deployed successfully'
    }

    failure {
        echo 'Build or deployment failed'
    }
}


}
