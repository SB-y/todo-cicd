pipeline {
    agent any

    environment {
        DOCKER_CMD = "docker"
        IMAGE_NAME = "planit-back"
    }

    stages {

        stage('1️⃣ Cloner le code backend') {
            steps {
                echo "📥 Clonage du dépôt Git..."
                git branch: 'main', url: 'https://github.com/SB-y/descodeuses-todoapp-backend.git'
            }
        }

        stage('2️⃣ Construire l’image Docker') {
            steps {
                echo "🏗️ Construction de l’image Docker..."
                sh "${DOCKER_CMD} build -t ${IMAGE_NAME} ."
            }
        }

        stage('3️⃣ Lancer les tests Selenium') {
            steps {
                echo "🧪 Exécution des tests Selenium..."
                dir('selenium') {
                    sh "npm ci"
                    sh "node test.js"
                }
            }
        }
    }

    post {
        success {
            echo "🎉 Pipeline exécuté avec succès !"
        }
        failure {
            echo "❌ Le pipeline a échoué."
        }
    }
}
