pipeline {
 stages{
        stage ('playbook') {         
           ansiblePlaybook ( 
             playbook: 'main.yml',
             inventory: 'inventory')
        }
        stage ('checkout') {
            steps {
             sh 'echo stage CHECKOUT'
             git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
            }
        }
        
        stage('build') {
            steps {
             sh 'echo stage BUILD'
             sh 'mvn -f pom.xml -s settings.xml compile'
            }
        }
        
        stage('test') {
            steps {
             sh 'echo stage TEST'
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
             sh 'echo stage DEPLOY'
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
