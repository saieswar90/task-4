pipeline {
    agent any

    parameters {
        extendedChoice(
            name: 'COMPONENTS',
            type: 'PT_CHECKBOX',
            description: 'Select components to deploy',
            value: 'frontend,backend,database',
            multiSelectDelimiter: ','
        )
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/saieswar90/task-4.git', branch: 'main'
            }
        }

        stage('Show Selected Components') {
            steps {
                echo "Selected: ${params.COMPONENTS}"
            }
        }

        stage('Deploy Components') {
            steps {
                script {
                    def selected = params.COMPONENTS.split(',')

                    if (selected.contains('frontend')) {
                        echo "🚀 Deploying FRONTEND"
                        bat '''
                        cd frontend
                        echo Running frontend...
                        '''
                    }

                    if (selected.contains('backend')) {
                        echo "⚙️ Deploying BACKEND"
                        bat '''
                        cd backend
                        echo Running backend...
                        '''
                    }

                    if (selected.contains('database')) {
                        echo "🗄️ Deploying DATABASE"
                        bat '''
                        cd database
                        echo Running DB script...
                        type init.sql
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ TASK-4 COMPLETED"
        }
        failure {
            echo "❌ TASK FAILED"
        }
    }
}
