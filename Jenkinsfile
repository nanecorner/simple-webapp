pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/nanecorner/simple-webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sh 'cp target/*.war $CATALINA_HOME/webapps/'
                sh '$CATALINA_HOME/bin/catalina.sh stop'
                sh '$CATALINA_HOME/bin/catalina.sh start'
            }
        }
        stage('Verify Deployment') {
            steps {
                script {
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://localhost:8081/simple-webapp/hello", returnStdout: true).trim()
                    if (response != '200') {
                        error "Deployment failed. Received HTTP response code: ${response}"
                    }
                }
            }
        }
    }
}
