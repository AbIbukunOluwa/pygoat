pipeline {
  
  agent any
  
  stages{
    stage("Preparation") {
      steps{
        // i want you to see this a working from terminal using jenkins
        // Installing python3 and virtual environment for python3
        sh 'sudo apt-get update && sudo apt-get install -y python3 python3-venv'
        sh 'sudo apt-get install -y libpq-dev'

        //creating virtual environment
        sh 'python3 -m venv venv'

        //From the virtual environment install the dependencies needed for the app
        sh '. venv/bin/activate && python3 -m pip install -U pip wheel setuptools'
        // sh 'python3 -m pip install -U pip wheel setuptools'
        sh '. venv/bin/activate && pip install -r requirements.txt'
      }
    }
  }
}
