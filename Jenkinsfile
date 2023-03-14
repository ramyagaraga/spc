pipeline {
    agent { label 'node1'} 
    stages {
        stage('vcs') { 
            steps {
                git url: 'https://github.com/ramyagaraga/spc.git',
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
                    sh 'mvn clean package sonar:sonar -Dsonar.login=58bc2abae0cef588fc418f417846217978e143b5 -Dsonar.organization=prspring -Dsonar.projectKey=prspring_spring'
                } 
            }
        } 
    }
}
