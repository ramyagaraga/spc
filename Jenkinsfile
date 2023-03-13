pipeline {
    agent { label 'node1'} 
    stages {
        stage('vcs') { 
            steps {
                git url: 'https://github.com/ramyagaraga/spring-petclinic.git',
                    branch: 'develop'

            }
        }
        stage('Build') { 
            steps {
                sh './mvnw package'
            } 
        } 
        stage('sonal analysis') {
            steps {  
                withSonarQubeEnv('sonar') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=ramyagaraga -Dsonar.ProjectKey=ramyagaraga_spc'
                } 
            }
        } 
    }
}
