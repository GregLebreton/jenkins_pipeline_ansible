pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages{

        stage ('checkout') {
            steps {
                git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
            }
        }

        stage ('playbook') {
            steps {
                ansiblePlaybook ( 
                    become: true,
                    credentialsId: 'vagrant',
                    installation: 'ansible',
                    inventory: 'inventory',
                    playbook: 'main.yml' )
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
        
        stage('deploy on NEXUS') {
            steps {
                sh 'mvn -f pom.xml -s settings.xml deploy'
            }
        }
    }
}
