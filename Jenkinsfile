pipeline {
    agent any
    
    environment {
        TESTING_ENVIRONMENT = "test_environment"
        PRODUCTION_ENVIRONMENT = "niraj_production"
        BUILD_TOOL = "Maven"
        UNIT_TEST_TOOL = "JUnit"
        INTEGRATION_TEST_TOOL = "Selenium"
        CODE_ANALYSIS_TOOL = "SonarQube"
        SECURITY_ANALYSIS_TOOL = "Snyk"
        DEPLOYMENT_TOOL = "DigitalOcean Droplet"
        NOTIFICATION_EMAIL = "nirajkhatiwada33@gmail.com"
    }
    
    stages {
        stage('Build') {
            steps {
                echo "Compiling the code and generating any necessary artifacts using ${BUILD_TOOL}"
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests using ${UNIT_TEST_TOOL}"
                echo "Running integration tests using ${INTEGRATION_TEST_TOOL}"
            }
                
            post {
                success {
                    mail(
                        subject: "Test Success: ${currentBuild.fullDisplayName}",
                        body: "Test executed successfully.",
                        to: "${NOTIFICATION_EMAIL}"
                    )
                }
                failure {
                    mail(
                        subject: "Test Failure: ${currentBuild.fullDisplayName}",
                        body: "Test execution failed.",
                        to: "${NOTIFICATION_EMAIL}"
                    )
                }
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code using ${CODE_ANALYSIS_TOOL}"
            }
        }
        stage('Security Analysis') {
            steps {
                echo "Checking the security of the code using ${SECURITY_ANALYSIS_TOOL}"
            }
                
            post {
                success {
                    mail(
                        subject: "Code security analysis Success: ${currentBuild.fullDisplayName}",
                        body: "Security analysis completed successfully.",
                        to: "${NOTIFICATION_EMAIL}"
                    )
                }
                failure {
                    mail(
                        subject: "Code security analysis Failure: ${currentBuild.fullDisplayName}",
                        body: "Security analysis failed.",
                        to: "${NOTIFICATION_EMAIL}"
                    )
                }
            }
        }
        stage('Deploy on Staging') {
            steps {
                echo "Deploying the application to a testing environment: ${TESTING_ENVIRONMENT} using ${DEPLOYMENT_TOOL}"
            }
        }
        stage('Integration test on Staging') {
            steps {
                script {
                    echo "Waiting for approval..."
                    sleep(time: 10, unit: 'SECONDS')
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment: ${PRODUCTION_ENVIRONMENT} using ${DEPLOYMENT_TOOL}"
            }
        }
    }
}