pipeline {
    agent {
        label 'agent-node'
        
    }
    stages {
        stage('Installer dépendances') {
            steps {
                git branch: 'main', url: 'https://github.com/FredericBellard/TP_Landingpage_deployment_cda.git'
            }
        }
        stage('contrôle qualité') {
            steps{
                sh """
               sonar-scanner \
                -Dsonar.projectKey=fred_TP_Landingpage_deployment_cda \
                -Dsonar.sources=. \
                -Dsonar.host.url=https://669b-212-114-26-208.ngrok-free.app \
                -Dsonar.token=${SonarToken}
                """
            }
        }
        stage('Déploiement') {
            steps {
                   sh """
                    lftp -d -u ${Login},${Mdp} ${Lienftp} -e "
                        mirror -R /home/jenkins/workspace/fred_TP_Landingpage_deployment_cda/ www/;
                        bye
                    "
                """             
            }
        }

    }
}
