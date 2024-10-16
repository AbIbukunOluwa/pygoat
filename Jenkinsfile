pipeline {
  
  agent any
  
  stages{
    stage("Preparation") {
      steps{
        // i want you to see this a working from terminal using jenkins
        // Installing python3 and virtual environment for python3
        sh 'sudo apt-get update && sudo apt-get install -y python3 python3-venv'

        //creating virtual environment
        sh 'python3 -m venv venv'

        //From the virtual environment install the dependencies needed for the app
        sh '. venv/bin/activate'
        sh 'python -m pip install -U pip wheel setuptools'
        sh 'pip install -r requirements.txt'
      }
    }
  }
}
