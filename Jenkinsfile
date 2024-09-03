pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sh 'scp target/*.war user@172.19.42.14:/opt/apache-tomcat-9.0.93/webapps/'
                sh 'ssh user@172.19.42.14 /opt/apache-tomcat-9.0.93/bin/shutdown.sh'
                sh 'ssh user@172.19.42.14 /opt/apache-tomcat-9.0.93/bin/startup.sh'
            }
        }
    }
}
