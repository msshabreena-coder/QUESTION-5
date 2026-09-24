pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pulls the code from your Git repository
                checkout scm
            }
        }

        stage('Parallel Checks') {
            parallel {
                stage('Run Unit Check') {
                    steps {
                        echo 'Starting Unit Check Stage...'
                        // Use bat instead of sh for Windows Jenkins agents
                        bat 'python unit_check.py'
                    }
                }
                stage('Run Integration Check') {
                    steps {
                        echo 'Starting Integration Check Stage...'
                        bat 'python integration_check.py'
                    }
                }
            }
        }

        stage('Summary') {
            steps {
                echo '=== Pipeline Execution Summary ==='
                echo 'All prior parallel stages executed successfully.'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: The entire pipeline completed smoothly!'
        }
        failure {
            echo 'FAILURE: One or more stages failed during execution.'
        }
    }
}

