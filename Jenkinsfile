pipeline {
    agent any
    stages {
        stage('Prepare Environment') {
            steps {
                // Установка Python и pip (для Ubuntu/Debian)
                sh '''
                  sudo apt-get update
                  sudo apt-get install -y python3 python3-pip
                '''
            }
        }
        stage('Checkout Source') {
            steps {
                // Клонирование репозитория проекта
                checkout scm
            }
        }
        stage('Install Requirements') {
            steps {
                // Установка зависимостей Python проекта
                sh 'pip3 install --upgrade pip'
                sh 'pip3 install -r requirements.txt || true'
            }
        }
        stage('Run Pytest') {
            steps {
                // Запуск тестов, создание отчёта JUnit XML
                sh 'pytest --junitxml=test-results.xml || true'
            }
            post {
                always {
                    // Публикация отчёта (если плагин JUnit установлен)
                    junit 'test-results.xml'
                }
            }
        }
    }
}
