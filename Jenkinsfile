pipeline {
    agent any
    stages {
        stage('Download Advice') {
            steps {
                script {
                    // JSON fájl letöltése a workspace mappába
                    sh 'curl -s "https://api.adviceslip.com/advice" -o advice.json'
                    sh 'cat advice.json'
                }
            }
        }
        stage('Extract and Check Advice') {
            steps {
                script {
                    // Advice kinyerése és mentése
                    sh 'cat ${env.WORKSPACE}/advice.json | jq -r .slip.advice > ${env.WORKSPACE}/advice.message'
                    
                    // Szóellenőrzés
                    sh '''
                        if [ $(wc -w < ${env.WORKSPACE}/advice.message) -gt 5 ]; then
                            echo "Advice has more than 5 words";
                        else
                            echo "Advice - $(cat ${env.WORKSPACE}/advice.message) has 5 words or less";
                            exit 1;
                        fi
                    '''
                }
            }
        }
            
        stage('Display Advice') {
            steps {
                script {
                    // Cowsay telepítése, ha szükséges
                    sh 'sudo apt-get install cowsay -y'
                    
                    // Mock Deploy - Advice megjelenítése
                    sh '''
                        /usr/games/cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1) < ${env.WORKSPACE}/advice.message
                    '''
                }
            }
        }
    }
}
