pipeline {
    agent { label 'node1'} 
    triggers { pollSCM ('* * * * *') } 
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') { 
            steps {
                git url: 'https://github.com/ramyagaraga/spc.git',
                    branch: 'release'

            }
        }
        stage('Build') { 
            steps {
                sh 'mvn package'
            }
        } 
        stage('sonal analysis') {
            steps {  
                withSonarQubeEnv('sonar') {
                    sh 'mvn clean package sonar:sonar -Dsonar.login=58bc2abae0cef588fc418f417846217978e143b5 -Dsonar.organization=prspring -Dsonar.projectKey=prspring_spring'
                     } 

            }
        } 
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true 
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
        stage('deployement') {
            steps { 
               sh 'ansible-playbook -i hosts spc.yml'
            }
        }
    }
}