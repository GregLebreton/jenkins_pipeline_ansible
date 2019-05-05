node {
    stage "checkout" 
        git branch: 'jenkins_ansible_maven_job', credentialsId: 'GregLebreton', url: 'https://github.com/GregLebreton/jenkins_pipeline_ansible.git'
    }

node{
    stage "playbook"
    sh 'echo playbook'
    ansiblePlaybook become: true, credentialsId: 'vagrant', installation: 'ansible', inventory: 'inventory', playbook: 'main.yml' ( 
        playbook: '${WORKSPACE}/main.yml',
            inventory: '${WORKSPACE}/inventory')
    }
 
node {
    stage "build"
        sh 'echo build'
        sh 'mvn -f pom.xml -s settings.xml compile'
    }

node {
    stage "test"
        sh 'echo test'
        sh 'mvn -f pom.xml -s settings.xml test'      
    }
 
node {
    stage "deploy"
        sh 'echo deploy'
        sh 'mvn -f pom.xml -s settings.xml deploy'
    }
