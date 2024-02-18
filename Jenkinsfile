pipeline {
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    
    agent any
    
    stages {
        stage('Checkout') {
            agent {
                label 'main'
            }
            steps {
                echo 'Cloning...'
                git 'https://github.com/tomilola75/ClassDemoProject.git'
            }
        }
        
        stage('Compile') {
            agent {
                label 'slave_1'
            }
            steps {
                echo 'Compiling...'
                sh 'mvn compile'
            }
        }
        
        stage('CodeReview') {
            agent {
                label 'slave_1'
            }
            steps {
                echo 'Code Review...'
                sh 'mvn pmd:pmd'
            }
        }
        
        stage('UnitTest') {
            agent {
                label 'slave_2'
            }
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Package') {
            agent {
                label 'main'
            }
            steps {
                echo 'Packaging...'
                sh 'mvn package'
            }
        }
    }
}

