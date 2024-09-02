pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Clona el repositorio desde Git
                git 'https://github.com/nanecorner/simple-webapp.git'
            }
        }
        stage('Build') {
            steps {
                // Ejecuta el comando para compilar el proyecto
                sh './mvnw clean package'
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
