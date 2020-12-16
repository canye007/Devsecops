pipeline{
    
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
    stages{
        stage('Checkout'){
            agent any
            steps{
                git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
            }
        }
        stage('Compile'){
            agent any
            steps{
                sh 'mvn compile'
            }
        }
         stage('CodeReview'){
             agent any
            steps{
                sh 'mvn pmd:pmd'
            }
           
        }
         stage('UnitTest'){
             agent {label 'linux_slave'}
            steps{
                git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
                sh 'mvn test'
            }
            
        }
         stage('MetricCheck'){
             agent any
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                always{
                    
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
         stage('Package'){
            agent {label 'linux_slave'}
            steps{
                sh 'mvn package'
            }
            
        }
    }
}
