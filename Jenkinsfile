pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Gitcheckout'){
            steps {
             checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '1', url: 'https://github.com/bandaribhanu/maven_java_project.git']]])   
            }
            }
                 stage('build') {
            steps {
                bat "mvn clean install"
            }
            }
                 stage('codequality') {
            steps {
                bat "mvn sonar:sonar"
            }
            }
                   stage('deploy') {
            steps {
               deploy adapters: [tomcat8(credentialsId: 'Tomcat1', path: '', url: 'http://localhost:7000/')], contextPath: 'maven_pipeline', war: '**/*.war'
             }
                   }
}
}
