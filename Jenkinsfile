pipeline {
    agent { label 'master' }
    stages {
        stage('Cloning the repo') {
            steps {
            	git credentialsId: '2aa4f82a-71ae-4d65-a850-e4fc7f22a09e', url: 'https://github.com/rajanshtha/java_custom_image.git'
            }
        }
        stage('Download amazon-corretto java') {
            steps {
            	sh 'wget https://d3pxv6yz143wms.cloudfront.net/8.232.09.1/amazon-corretto-8.232.09.1-linux-x64.tar.gz'
            }
        }
        stage('Repack the org custom certs') {
            steps {
            	sh '''
            	tar -xvf amazon-corretto-8.232.09.1-linux-x64.tar.gz
            	cp regeneron-ca.crt amazon-corretto-8.232.09.1-linux-x64/jre/lib/security/regeneron-ca.crt
            	tar -cvf amazon-corretto-8.232.09.1-linux-x64.tar.gz amazon-corretto-8.232.09.1-linux-x64
            	'''
            }
        }
        stage('building docker image') {
            steps {
            	sh 'docker build -t nginx:corretto .'
            	cleanWs()
            }
        }
    }
}

