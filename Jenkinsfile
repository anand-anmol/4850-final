/*
Name: Anmol Anand - A01174846
Date: December 8, 2021
Description: TODO
 */

pipeline{
    agent any
    parameters {
        booleanParam(defaultValue: false, description: 'Run Unit Tests', name: 'TEST') 
    }
    stages {
        stage('Build') {
            steps {
                echo "Student Number: A01174846"
                echo "Group Number: 21"
                echo "Installing the Python Requirements..."
                sh 'pip3 install -r requirements.txt'
                echo "Requirement complete"
            }
        }
        stage('Code Quality') {
            steps {
                sh 'pylint-fail-under --fail_under 7 *.py'
            }
        }
        stage('Code Quantity') {
            steps {
                sh 'echo "Number of Python files in project: $(ls *.py | wc -l)"'
            }
        }
        stage('Test') {
            when {
                expression { params.TEST }
            }
            steps {
                script {
                    sh 'python3 test_book_manager.py'
                    post {
                        always {
                            script {
                                def test_reports_exist = fileExists 'test-reports'
                                if (test_reports_exist) {                        
                                    junit 'test-reports/*.xml'
                                }
                            }
                        }
                    }
                }
            }
        }
        stage('Package') {
            steps {
                sh 'zip package.zip *.py'
                archiveArtifacts artifacts: 'package.zip'
            }
        }
    }
}
