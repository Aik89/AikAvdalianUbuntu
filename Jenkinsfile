pipeline {
    agent any

    stages {
        stage('Checkout main repo') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Aik89/AikAvdalianUbuntu.git',
                        credentialsId: 'YOUR_CREDENTIAL_ID'
                    ]]
                ])
            }
        }

        stage('Checkout RamatGan repo') {
    steps {
        checkout([$class: 'GitSCM',
            branches: [[name: 'main']],
            userRemoteConfigs: [[
                url: 'https://github.com/Aik89/RamatGan.git',
                credentialsId: 'RamatGanToken'
            ]]
        ])
    }
}


        stage('Setup Python') {
            steps {
                sh 'python3 -m venv venv'
                sh 'source venv/bin/activate && pip install -r requirements.txt || true'
            }
        }

        stage('Run Daily Tests') {
            steps {
                sh 'source venv/bin/activate && pytest RamatGan/tests/daily_check/test_daily.py'
            }
        }
    }
}
