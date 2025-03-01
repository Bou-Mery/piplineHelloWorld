pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                node {
                    echo '📥 Clonage du dépôt...'
                    git branch: 'master', url: 'https://github.com/Bou-Mery/piplineHelloWorld.git'
                }
            }
        }

        stage('Build') {
            steps {
                node {
                    echo '🔧 Compilation du projet...'
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                node {
                    echo '🧪 Exécution des tests...'
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                node {
                    echo '🚀 Déploiement de l\'application...'
                    script {
                        def jarFile = sh(script: "ls target/*.jar", returnStdout: true).trim()
                        if (jarFile) {
                            sh "java -jar ${jarFile}"
                        } else {
                            error "🚨 Aucun fichier .jar trouvé dans le dossier target/"
                        }
                    }
                }
            }
        }
    }
}
