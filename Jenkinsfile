pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Check out the code from your version control system
                git branch: 'dev/taj', url: 'https://github.com/taj-DevOps/python-webapp.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Use a virtual environment for isolation
                script {
                    sh 'python3 -m venv venv'
                    sh '. ${WORKSPACE}/venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                // Run your Python tests
                script {
                    sh 'python3 -m unittest discover'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Your deployment steps go here
                script {
                    // For example, copy your application files to a server
                    sh 'python3 app.py &'
                }
            }
        }
    }
    
    post {
        always {
            // Clean up (optional)
            sh 'exit' // deactivate the virtual environment
        }
    }
}
