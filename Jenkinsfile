pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }
        stage('Create Folder') {
            steps {
                sh 'mkdir -p new_folder'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('your-image-name')
                }
            }
        }
        stage('Push to GitHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-credentials', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh '''
                        git config --global user.email "you@example.com"
                        git config --global user.name "Your Name"
                        git add new_folder
                        git commit -m "Add new folder"
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/your-username/your-repo.git
                    '''
                }
            }
        }
    }
}
