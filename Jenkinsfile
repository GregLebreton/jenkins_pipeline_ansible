pipeline {
 stages{
    stage ('playbook') {
      steps {
        ansiblePlaybook ( 
            playbook: 'main.yml',
            inventory: 'inventory')
      }
    }

    stage ('deploy') {
        steps {
            git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
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
