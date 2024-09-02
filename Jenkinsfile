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
                // Usa mvn para compilar el proyecto
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                // Copia el archivo WAR a Tomcat y reinicia el servidor
                sh 'cp target/*.war $CATALINA_HOME/webapps/'
                sh '$CATALINA_HOME/bin/catalina.sh restart'
            }
        }
    }
}
