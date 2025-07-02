pipeline {
    agent any

    environment {
        CONTROL_NODE = '54.234.3.247' 
        SSH_KEY = credentials('ansible-key') 
    }

    stages {
        stage('Prepare Control Node') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no -i $SSH_KEY ubuntu@$CONTROL_NODE 'sudo apt update && sudo apt install -y ansible python3 python3-pip'
                ssh -i $SSH_KEY ubuntu@$CONTROL_NODE 'pip3 install boto3'
                '''
            }
        }

        stage('Copy Files to Control Node') {
            steps {
                sh '''
                scp -i $SSH_KEY ansible.cfg inventory.yml playbook.yml app.tar.gz ubuntu@$CONTROL_NODE:/home/ubuntu/
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ssh -i $SSH_KEY ubuntu@$CONTROL_NODE 'ANSIBLE_CONFIG=/home/ubuntu/ansible.cfg ansible-playbook -i /home/ubuntu/inventory.yml /home/ubuntu/playbook.yml'
                '''
            }
        }
    }
}

