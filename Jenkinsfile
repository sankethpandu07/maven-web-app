pipeline {
    agent any
    
    stages {
        stage('GetCode') {
            steps {
                // Fetch code from the GitHub repository
                git url: 'https://github.com/nenavathsrinu/maven-web-app.git'
            }
        }
        
        stage('Git Pull') {
            steps {
                // Pull code from the Git repository
                git branch: 'master', credentialsId: 'your_git_credentials', url: 'https://github.com/nenavathsrinu/maven-web-app.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build your project (e.g., Maven or Gradle)
                bat 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv('sonar-9') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                // Deploy the WAR file to Tomcat
                deploy adapters: [tomcat9(credentialsId: 'tomcat-123', url: 'http://192.168.0.170:8080/')],
                       contextPath: '/opt/apache-tomcat-9.0.88/webapps',
                       war: 'target/maven-web-app.war'  // Use forward slashes for file paths
            }
        }
    }
}
