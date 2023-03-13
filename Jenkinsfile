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
                    branch: 'feature'

            }
        }
        stage('Build') { 
            steps {
                sh './mvnw package'
            }
        } 