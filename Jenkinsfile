pipeline {
    agent none

    stages {
        stage('Initialize Workspace') {
            agent any
            steps {
                echo 'Repository cloned and workspace initialized.'
            }
        }

        stage('Execute Python Automation') {
            agent {
                docker { 
                    image 'python:3.11-slim' 
                    reuseNode true
                }
            }
            steps {
                echo 'Starting Python container...'
                sh 'python --version'
                // sh 'python scripts/your_automation_script.py'
            }
        }

        stage('Execute PowerShell Tasks') {
            agent {
                docker { 
                    image 'mcr.microsoft.com/powershell:lts-ubuntu-22.04' 
                    reuseNode true
                }
            }
            steps {
                echo 'Starting PowerShell container...'
                sh '''
                    pwsh -Command 'Write-Host "PowerShell container active."; $PSVersionTable.PSVersion'
                '''
                // pwsh -File scripts/your_task.ps1
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution finished. Cleaning up workspace...'
            cleanWs()
        }
    }
}
