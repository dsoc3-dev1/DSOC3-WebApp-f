pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
               git url: 'https://github.com/dsoc3-dev1/DSOC3-WebApp-f.git', branch: 'main'
            }
        }
        stage('compile') {
            steps {
                sh '''
                mvn clean compile
                tree target
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                tree target
                mvn test
                tree target
                '''
            }
        }
        stage('Build') {
            steps {
                sh '''
                tree target
                mvn package
                tree target
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                sudo cp target/dsoc3-webapp.war /var/lib/tomcat10/webapps/
                '''
            }
        }
    }
}
