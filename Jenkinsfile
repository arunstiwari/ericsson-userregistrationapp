pipeline {
    agent { 
                label 'mac'
            }
    stages {
        
        stage('Unit Test') {
            agent { 
                label 'mac'
            }
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
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