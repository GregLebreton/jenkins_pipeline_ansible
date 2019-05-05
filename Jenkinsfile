 node {
    ansiblePlaybook ( 
        playbook: 'main.yml',
        inventory: 'inventory.ini')
}

node {
     agent any
    options {
        retry(3)
    }
    tools {
        maven 'maven' 
    }
    stages {
        stage('checkout') {
            steps {
                git branch: 'ansible_maven_deploy', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/Maven-Jenkinsfile.git'
            }
        }
        
        stage('build') {
            steps {
                sh 'mvn -f pom.xml -s settings.xml compile'
            }
        }
        
        stage('test') {
            steps {
                sh 'mvn -f pom.xml -s settings.xml test'
            }
            
        }
        
        stage('deploy') {
            when {
                allOf {
                    stage 'test' == SUCCESS
                }           
            }
            steps {
                sh 'mvn -f pom.xml -s settings.xml deploy'
            }
        }
    }
    post {
        success {
            echo "Builded and deployed successfully"
        }
        failure {
            echo "Oh no: build failure"
        }
    }
}
