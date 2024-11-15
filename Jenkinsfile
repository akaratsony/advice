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
                    
                    // Szóellenőrzés
                    sh '''
                        if [ $(wc -w < ${WORKSPACE}/advice.message) -gt 5 ]; then
                            echo "Advice has more than 5 words";
                        else
                            echo "Advice - $(cat ${WORKSPACE}/advice.message) has 5 words or less";
                            exit 1;
                        fi
                    '''
                }
            }
        }
            
        stage('Display Advice') {
            steps {
                script {
                    // Mock Deploy
                    sh ''' sudo apt get install cowsay -y''''
                    sh ''' export PATH="$PATH:/usr/games:/usr/local/games" '''
                    sh '''
                        cat ${WORKSPACE}/advice.message | /usr/games/cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1)
                    '''
                }
            }
        }
    } // <-- Ez a zárójel hiányzott
}
