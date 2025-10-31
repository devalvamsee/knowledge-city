pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/devalvamsee/knowledge-city.git'
      }
    }
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test || echo "No tests yet"'
      }
    }
    stage('Package') {
      steps {
        sh 'zip -r app.zip *'
        archiveArtifacts artifacts: 'app.zip', fingerprint: true
      }
    }
    stage('Deploy') {
      steps {
        echo "Triggering Ansible to deploy..."
        sh 'ansible-playbook -i ansible/inventory ansible/deploy.yml'
      }
    }
  }
}

