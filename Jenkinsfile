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
                sh '/usr/local/bin/mvn test'
            }
            
        }
        stage('Mutation Test') {
            agent { 
                label 'mac'
            }
            steps {
                sh '/usr/local/bin/mvn org.pitest:pitest-maven:mutationCoverage'
            }
        }
        stage('Checkstyle Analysis') {
            agent { 
                label 'mac'
            }
            steps {
                sh '/usr/local/bin/mvn checkstyle:checkstyle'
            }
        }
        stage('Code Coverage Analysis') {
            agent { 
                label 'mac'
            }
            steps {
                sh '/usr/local/bin/mvn jacoco:report'
            }
            post {
                always {
                    jacoco( 
      					execPattern: 'target/*.exec',
      					classPattern: 'target/classes',
      					sourcePattern: 'src/main/java',
      					exclusionPattern: 'src/test*'
					)
                }
            }
        }
    }
}