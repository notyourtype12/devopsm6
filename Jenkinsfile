node {

    checkout scm

    stage("Build") {
        docker.image('composer:2').inside('-u root') {
            sh 'composer install'
        }
    }

    stage("Testing") {
        sh 'echo "Testing pipeline Laravel"'
    }

    stage("Deploy Production") {
        sh 'ansible-playbook deploy.yml -i inventory'
    }

}