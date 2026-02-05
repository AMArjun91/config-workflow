pipeline {
  parameters {
    choice(name: 'ENV', choices: ['dev', 'stage', 'prod'], description: '')
  }

  stages {
    stage('Deploy THD') {
      when {
        expression { params.ENV == 'prod' || params.ENV == 'stage' }
      }
      steps {
        echo "Deploying THD"
      }
    }

    stage('Deploy KFI') {
      when {
        expression { params.ENV == 'prod' }
      }
      steps {
        echo "Deploying KFI"
      }
    }

    stage('Deploy REVOLTAB') {
      when {
        expression { params.ENV == 'prod' }
      }
      steps {
        echo "Deploying REVOLTAB"
      }
    }
  }
}
