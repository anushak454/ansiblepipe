pipeline {
    agent none // Define no initial agent (run on specific node later)

    stages {
        stage('Install Ansible on node1') {
            agent any // Run this stage on any available Jenkins agent
            steps {
                ssh(credentialsId: 'root/anusha@1993', label: 'node1', wait: true) { // Use credentials for node1
                    sh 'sudo apt update && sudo apt install -y ansible' // Install Ansible on node1
                }
            }
        }
        stage('Run Ansible Playbook') {
            agent any // Run this stage on any available Jenkins agent (can be optimized to run on node1)
            steps {
                script {
                    def playbookName = 'install_docker_and_webserver.yml' // Playbook name
                    sh "ansible-playbook -i hosts ${playbookName}" // Run playbook targeting 'hosts' inventory
                }
            }
        }
    }
}
