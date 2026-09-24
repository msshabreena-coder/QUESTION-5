pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // If using a Git repository, this pulls the code. 
                // For a local pipeline job, 'checkout scm' handles it automatically.
                checkout scm
            }
        }

        stage('Parallel Checks') {
            parallel {
                stage('Run Unit Check') {
                    steps {
                        echo 'Starting Unit Check Stage...'
                        sh 'python3 unit_check.py'
                    }
                }
                stage('Run Integration Check') {
                    steps {
                        echo 'Starting Integration Check Stage...'
                        sh 'python3 integration_check.py'
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
            echo '🎉 SUCCESS: The entire pipeline completed smoothly!'
        }
        failure {
            echo '❌ FAILURE: One or more stages failed during execution.'
        }
    }
}
