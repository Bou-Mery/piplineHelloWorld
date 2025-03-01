pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Clonage du dépôt...'
                git branch: 'master', url: 'https://github.com/Bou-Mery/piplineHelloWorld.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔧 Compilation du projet...'
                sh 'mvn clean install'  // Utilisation de install pour éviter des problèmes avec les dépendances
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Exécution des tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Déploiement de l\'application...'
                script {
                    def jarFile = sh(script: "ls target/*.jar", returnStdout: true).trim()
                    if (jarFile) {
                        echo "📦 Fichier trouvé : ${jarFile}"
                        sh "java -jar ${jarFile}"
                    } else {
                        error "🚨 Aucun fichier .jar trouvé dans le dossier target/"
                    }
                }
            }
        }
    }
}
