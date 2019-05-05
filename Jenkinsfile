node {
    stage "checkout" 
        git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
    }

node{
    stage "playbook"
    ansiblePlaybook ( 
        become: true,
        credentialsId: 'vagrant',
        installation: 'ansible',
        inventory: 'inventory',
        playbook: 'main.yml' )
    }
 
node {
    tools {
        maven 'maven' 
    }
    stage "build"
        sh 'mvn -f pom.xml -s settings.xml compile'
    }

node {
    stage "test"
        sh 'mvn -f pom.xml -s settings.xml test'      
    }
 
node {
    stage "deploy"
        sh 'mvn -f pom.xml -s settings.xml deploy'
    }
