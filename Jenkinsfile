pipeline {
    agent { label 'node1'} 
    stages {
        stage('vcs') { 
            steps {
                git url: 'https://github.com/ramyagaraga/spring-petclinic.git',
                    branch: 'feature'

            }
        }
        stage('Build') { 
            steps {
                sh './mvnw package'
            }
        }
    }
}
