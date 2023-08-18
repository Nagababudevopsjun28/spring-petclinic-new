pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Nagababudevopsjun28/spring-petclinic-new.git',
                    branch: 'main'
            }
        }
            stage('package') {
                tools {
                     jdk 'JDK_17'
                }
                steps {
                    sh "mvn ${params.MAVEN_GOAL}"
                }
            }    
            stage('sonar analysis') {
                  steps {
                    // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                    withSonarQubeEnv('SONAR_CLOUD') {
                        // requires SonarQube Scanner for Maven 3.2+ 
                        // sh 'mvn clean package sonar:sonar -Dsonar.organization=siva_key'
                    }    
                }
            }
        }
    }
}        
        
       