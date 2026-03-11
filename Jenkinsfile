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
        docker.image('agung3wi/alpine-rsync:1.1').inside("-u root") {
            sshagent (credentials: ['ssh-prod']) {
                sh "mkdir -p ~/.ssh"
                sh "ssh-keyscan -H $PROD_HOST > ~/.ssh/known_hosts"
                sh "rsync -rav --delete ./laravel/ ajiiee@$PROD_HOST:/home/ubuntu/prod.kelasdevops.xyz/ --exclude=.env --exclude=storage --exclude=.git"
            }
        }
    }

}