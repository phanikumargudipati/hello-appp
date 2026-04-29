pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/phanikumargudipati/hello-appp.git'
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                call "C:\\Tomcat\\apache-tomcat-11.0.21-windows-x64\\apache-tomcat-11.0.21\\bin\\shutdown.bat"

                ping 127.0.0.1 -n 10 > nul

                del /Q "C:\\Tomcat\\apache-tomcat-11.0.21-windows-x64\\apache-tomcat-11.0.21\\webapps\\hello-app.war"

                rmdir /S /Q "C:\\Tomcat\\apache-tomcat-11.0.21-windows-x64\\apache-tomcat-11.0.21\\webapps\\hello-app"

                copy "target\\hello-app.war" "C:\\Tomcat\\apache-tomcat-11.0.21-windows-x64\\apache-tomcat-11.0.21\\webapps\\"

                cmd /c start "" "C:\\Tomcat\\apache-tomcat-11.0.21-windows-x64\\apache-tomcat-11.0.21\\bin\\startup.bat"
                '''
            }
        }
    }
}