pipeline{
    tools{
        jdk 'jdk8maven'
        maven 'mymaven'
    }
    
    agent none
    stages{stage('Checkout'){
                agent any
                steps{
                    sh 'mvn compile'
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
                post{
                    always{
                        pmd pattern: 'target/pmd.xml'
                    }
                }
            }
            stage('UnitTest'){
                agent {label 'amrutawin_slave'}
                steps{
                    git 'https://github.com/amrutabhanushali011019911/devopsproject.git'
                    bat 'mvn test'
                }
                post{
                    always{
                        junit 'target/surefire-reports/*.xml'
                    }
                }
                
            }
            stage('MetricCheck'){
                agent any
                steps{
                    
                    git 'https://github.com/amrutabhanushali011019911/devopsproject.git'
              
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    always{
                        
                        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    }
                }
            }
            stage('Package'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
    }
}
