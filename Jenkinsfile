pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21"
        JOB_NAME = "CustomerLoggerJob"
    }

    parameters {
        string(name: 'CSV_FILE_PATH', defaultValue: 'C:/Users/krish/Downloads/Talend/customers.csv')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Krishnachaitanya2408/talendCICDExample.git'
            }
        }

        stage('Unzip Job') {
            steps {
                bat 'powershell -Command "Expand-Archive -Force CustomerLoggerJob_0.1.zip .\\job_folder"'
            }
        }

        stage('Run Talend Job') {
            steps {
                bat '''
                cd job_folder\\CustomerLoggerJob
                call CustomerLoggerJob_run.bat --context=Default ^
                --context_param CSV_FILE_PATH=%CSV_FILE_PATH% ^
                '''
            }
        }
    }
}
