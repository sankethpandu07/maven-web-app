pipeline {
    agent any
    
    environment {
        // Adjusted Maven path to include the bin directory
        PATH = "${PATH};C:/Program Files/maven/apache-maven-3.9.6/bin"
    }
    
    stages {
        stage('GetCode') {
            steps {
                // Fetch code from the GitHub repository
                git url: 'https://github.com/sankethpandu07/maven-web-app.git'
            }
        }
        
        stage('Build') {
            steps {
                // Use Maven to clean and package the code
                bat 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis
                withSonarQubeEnv('sonar-9') {
                    bat "mvn sonar:sonar"
                }
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                // Deploy the WAR file to Tomcat
                deploy adapters: [tomcat9(credentialsId: 'tomcat', url: 'http://172.31.8.203:8080/')],
                       contextPath: '/opt/apache-tomcat-9.0.90/webapps',
                       war: 'target/maven-web-app.war'  // Use forward slashes for file paths
            }
        }
    }
}
