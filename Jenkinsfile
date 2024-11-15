pipeline {
    agent any
    stages {
        stage('Download Advice') {
            steps {
                script {
                    // JSON fájl letöltése a home könyvtárba
                    sh 'curl -s "https://api.adviceslip.com/advice" -o advice.json'
                    sh 'cat advice.json'
                }
            }
        }
        stage('Extract and Check Advice') {
            steps {
                script {
                    // Advice kinyerése és mentése
                    sh 'cat ${WORKSPACE}/advice.json | jq -r .slip.advice > ${WORKSPACE}/advice.message'
                    
           
                }
            }
        }
       
    }
}
