pipeline{
  agent any
  environment{
    PYTHON_PATH='C:\Program Files\Python311;C:\Program Files\Python311\Scripts'
  }
  stages{
    stage('Checkout'){
      steps{
        checout scm
      }
    }
    stage('build'){
      steps{
        bat '''
        set PATH=%PYTHON_PATH%;%PATH%
        pip install -r requirements.txt
        '''
      }
    }
    stage('SonarAnalysis'){
      environment{
        SONAR_TOKEN=credentials('sonarqube-token')
      }
      steps{
        bat '''
        set PATH=%PYTHON_PATH%;%PATH%
        sonar-scanner -Dsonar.projectKey=sonartest4
        -Dsonar.sources=. 
        -Dsonar.host.url=http://localhost:9000 
        -Dsonar.token=%SONAR_TOKEN%
        '''
      }
    }
  }
  POST{
    success{
      echo "well went and good"
    }
    failure{
      echo "failed"
    }
  }
  
}



