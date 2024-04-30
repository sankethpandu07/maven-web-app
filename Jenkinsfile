pipeline {
    agent any
    environment {
        PATH = "$PATH:C:/Program Files/maven/apache-maven-3.9.6/bin" // Fixed the syntax error here and added the missing closing quote
    }
    stages {
        stage('getcode') { // Enclosed stage names in quotes
            steps {
                git branch: 'master', // Added a comma between branch and URL
                    url: 'https://github.com/nenavathsrinu/maven-web-app.git' // Corrected the structure of git step
            }
        }
        stage('build') { // Enclosed stage names in quotes
            steps {
                sh 'mvn clean package' // Removed the unnecessary 'mvn' within the string
            }
        }
    }
}
