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
                sh '${MAVEN_HOME} test'
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