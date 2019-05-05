node {
    stage "checkout" 
        git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
    }

node{
    stage "playbook"
    sh 'launching playbook'
    ansiblePlaybook ( 
        become: true,
        credentialsId: 'vagrant',
        installation: 'ansible',
        inventory: 'inventory',
        playbook: 'main.yml' )
    }
 
node {
    stage "build"
        sh 'launching build'
        sh 'mvn -f pom.xml -s settings.xml compile'
    }

node {
    stage "test"
        sh 'launching test'
        sh 'mvn -f pom.xml -s settings.xml test'      
    }
 
node {
    stage "deploy"
        sh 'launching deploy'
        sh 'mvn -f pom.xml -s settings.xml deploy'
    }
