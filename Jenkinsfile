def MAVEN_HOME
pipeline {
    agent { 
                label 'mac'
            }
    stages {
    
    	stage('Initialize the variables') {
            // Each stage is made up of steps
            steps{
                script{
                    MAVEN_HOME="/usr/local/bin/mvn"
                }
            }                
        }
        
        stage('Unit Test') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn test'
            }
            
        }
        stage('Mutation Test') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn org.pitest:pitest-maven:mutationCoverage'
            }
        }
        stage('Checkstyle Analysis') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('Code Coverage Analysis') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn jacoco:report'
            }
            post {
                always {
                    step([
		              $class           : 'JacocoPublisher',
		              execPattern      : 'target/jacoco.exec',
		              classPattern     : 'target/classes/main',
		              sourcePattern    : 'src/main/java',
		              exclusionPattern : '**/*Test.class'
		          ])
                }
            }
        }
        stage('Sonarqube Analysis') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://54.72.251.138:9000'
            }
        }
        
    }
}
