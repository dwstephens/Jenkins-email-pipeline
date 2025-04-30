pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                echo "Checkout the source code from Git repository"
                echo "Installing cibuildwheel package"
                echo "Build wheel files"
                echo "Archive wheel files"
            }
        }
        stage('Unit and Integration Tests'){
            steps{
                script {
                    def logFile = "test.log"
                    // Create/clear the log file
                    sh "echo 'Unit and Integration Tests Started' > ${logFile}"
                    
                    // Function to log messages to both console and file
                    def logMessage = { message ->
                        echo message
                        sh "echo '${message}' >> ${logFile}"
                    }
                    logMessage "Creating virtual environment"
                    logMessage "Installing requirements and wheel files"
                    logMessage "Executing pytest unit tests"
                    logMessage "Executing pytest integration tests"
                    logMessage "Remove virtual environment"
                }
            }
            post {
                always {
                    emailext attachmentsPattern: '**/test.log',
                        to: "s225259172@deakin.edu.au",
                        subject: "${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: "Unit and Integration Tests stage ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        mimeType: 'text/html'
                }
            }
        }
        stage('Code Analysis'){
            steps{
                echo "Creating virtual environment"
                echo "Installing pylint and flake 8"                                
                echo "Linting the code with pylint"
                echo "Checking for compliance with flake8"
                echo "Remove virtual environment"
            }
        }
        stage('Security Scan'){
            steps{
                script {
                    def logFile = "security_scan.log"
                    // Create/clear the log file
                    sh "echo 'Security Scan Started' > ${logFile}"
                    
                    // Function to log messages to both console and file
                    def logMessage = { message ->
                        echo message
                        sh "echo '${message}' >> ${logFile}"
                    }
                    logMessage "Creating virtual environment"
                    logMessage "Installing bandit"
                    logMessage "Running bandit"
                    logMessage "Remove virtual environment"
                }
                echo "Creating virtual environment"
                echo "Installing bandit"
                echo "Running bandit"
                echo "Remove virtual environment"
            }
            post {
                always {
                    emailext attachmentsPattern: '**/security_scan.log',
                        to: "s225259172@deakin.edu.au",
                        subject: "${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: "Security scan stage ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        mimeType: 'text/html'
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "Deploy the application to the staging environment using AWS CodeDeploy"
            }
        }
        stage('Integration Tests on Staging '){
            steps{
                echo "Polling for deployment success"
                echo "Logged into instance"
                echo "Creating virtual environment"
                echo "Installing requirements and wheel files"
                echo "Running Integration tests"
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Waiting for manual approval to deploy the code to the production environment"
                sleep 10
                echo "Deploy the application to the production environment using AWS CodeDeploy"
                sleep 10
            }
        }
    }
}