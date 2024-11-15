pipeline {
    agent any
    stages {
        stage('Create File') {
            steps {
                script {
                    // Fájl létrehozása a home könyvtárban
                    sh 'curl -s "https://api.adviceslip.com/advice" -o advice.json'
                    sh 'cat advice.json'
                }
            }
        }
    }
}
