pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Nagababudevopsjun28/spring-petclinic.git',
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
                  withSonarQubeEnv('SONAR_CLOUD') {
                       sh 'mvn clean package sonar:sonar'

                    }   

                } 
                stage('post build') {
                    steps {
                        archiveArtifacts artifacts: '**/target/spring-petclinic-3.1.0-SNAPSHOT.jar',
                                         onlyIfsuccessful: true
                        junit testResults: '**/surefire-reports/TEST-*.xml' 

                    }
                }
            }      

        } 
    }                                


                
                
        


 