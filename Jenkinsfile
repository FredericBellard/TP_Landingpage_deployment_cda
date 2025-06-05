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
