pipeline {
    agent any

    environment {
        CONTROL_NODE = '54.234.3.247'
    }

    stages {

        stage('Add Control Node to known_hosts') {
            steps {
                sshagent (credentials: ['ansible-key']) {
                    sh '''
                        mkdir -p ~/.ssh
                        ssh-keyscan -H $CONTROL_NODE >> ~/.ssh/known_hosts
                    '''
                }
            }
        }

        stage('Prepare App Archive') {
            steps {
                sh 'tar -czvf app.tar.gz app/'
            }
        }

        stage('Install Dependencies on Control Node') {
            steps {
                sshagent (credentials: ['ansible-key']) {
                    sh '''
                        ssh ubuntu@$CONTROL_NODE '
                            sudo apt update &&
                            sudo apt install -y ansible python3 python3-pip
                        '
                    '''
                }
            }
        }

        stage('Copy Files to Control Node') {
            steps {
                sshagent (credentials: ['ansible-key']) {
                    sh '''
                        scp app.tar.gz ansible.cfg inventory.yml playbook.yml ubuntu@$CONTROL_NODE:/home/ubuntu/
                    '''
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sshagent (credentials: ['ansible-key']) {
                    sh '''
                        ssh ubuntu@$CONTROL_NODE '
                            ANSIBLE_CONFIG=/home/ubuntu/ansible.cfg
                            ansible-playbook -i /home/ubuntu/inventory.yml /home/ubuntu/playbook.yml
                        '
                    '''
                }
            }
        }
    }
}

