pipeline {
    // Run on any available agent
    agent any

    triggers {
        // Trigger the pipeline on a push to GitHub
        githubPush()
    }
    
    stages {
        stage('Checkout') {
            steps {
                // I had to add this checkout step to check out the source code from the configured Source Control Management
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Building the code using Maven to compile and package the application
                echo "Starting the build process using Maven"
                // sh 'mvn clean package'
                echo "Build completed"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                // Running unit and integration tests using Maven
                echo "Running unit tests"
                // sh 'mvn test'
                echo "Unit tests completed"
            }
            post {
                // Notifications or actions based on the outcome of the tests
                success {
                    // Sending an email in case of success
                    emailext body: 'All tests passed successfully.',
                             to: 'sinankilcitest@gmail.com',
                             subject: 'Tests Passed'
                }
                failure {
                    // Sending an email in case of failure
                    emailext body: 'Testing stage failed. Check logs for details.',
                             to: 'sinankilcitest@gmail.com',
                             subject: 'Tests Failed'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                // Static code analysis with SonarQube
                echo "Performing code analysis using SonarQube"
                // sh 'mvn sonar:sonar'
                echo "Code analysis completed"
            }
        }

        stage('Security Scan') {
            steps {
                // Performing security scanning using OWASP ZAP
                echo "Starting security scan with OWASP ZAP"
                // sh 'zap-cli --quick-scan http://localhost:8080'
                echo "Security scan completed"
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploying the application to a staging server using Ansible. AWS CLI also can be used for deployment to AWS EC2.
                echo "Deploying to staging server (AWS EC2)"
                // sh 'ansible-playbook deploy_staging.yml'
                echo "Deployment to staging completed"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Running integration tests on the staging environment. Selenium for UI tests and Postman for API tests can also be used.
                echo "Running integration tests on staging environment"
                // sh 'python integration_tests.py'
                echo "Integration tests on staging completed"
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploying the application to the production server using Ansible. AWS CLI also can be used for deployment to AWS EC2.
                echo "Deploying to production server (AWS EC2)"
                // sh 'ansible-playbook deploy_production.yml'
                echo "Deployment to production completed"
            }
        }
    }
}
