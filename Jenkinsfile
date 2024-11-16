pipeline {
    agent any
    environment {
        PYTHON_VERSION = 'python3.12' // Specify Python version
        VENV_DIR = 'venv'            // Virtual environment directory
    }
    stages {
        stage('Setup') {
            steps {
                echo 'Setting up Python environment'
                sh '''
                bash -c "
                # Ensure the correct Python version is being used
                ${PYTHON_VERSION} --version

                # Create virtual environment
                ${PYTHON_VERSION} -m venv ${VENV_DIR}

                # Activate virtual environment
                source ${VENV_DIR}/bin/activate

                # Upgrade pip to the latest version
                pip install --upgrade pip

                # Install dependencies
                pip install -r requirements.txt
                "
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests in virtual environment'
                sh '''
                bash -c "
                # Activate virtual environment
                source ${VENV_DIR}/bin/activate

                # Run your test script or commands
                python -c \\"print('Hello from Jenkins Pipeline with Python!')\\"
                "
                '''
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace'
            sh '''
            # Clean up the virtual environment
            rm -rf ${VENV_DIR}
            '''
        }
    }
}
