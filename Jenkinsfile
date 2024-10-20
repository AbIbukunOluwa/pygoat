pipeline {
  
  agent any
  
  stages{
    stage("Preparation") {
      steps{
        // i want you to see this a working from terminal using jenkins
        // Installing python3 and virtual environment for python3
        sh 'sudo apt-get update && sudo apt-get install -y python3 python3-venv'
        sh 'sudo apt-get install -y libpq-dev'
        sh 'sudo apt-get install -y python3-dev python3-setuptools'
        sh 'sudo apt-get install -y libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python3-tk libharfbuzz-dev libfribidi-dev libxcb1-dev'

        //creating virtual environment
        sh 'python3 -m venv venv'

        //From the virtual environment install the dependencies needed for the app
        sh '. venv/bin/activate && python3 -m pip install -U pip wheel setuptools'
        sh '. venv/bin/activate && pip install -r requirements.txt'
      }
    }

    // stage ("Check Information Disclosure") {
    //   steps{
    //     Now I will be performing a scan on secrets exposed by this repo.
    //     sh 'rm exposed || true'
    //     remove the file exposed if there is and if there isn't forget about it.
    //     sh 'docker run trufflesecurity/trufflehog git https://github.com/AbIbukunOluwa/pygoat.git --json > exposed'
    //     sh 'trufflehog git https://github.com/AbIbukunOluwa/pygoat.git --json > exposed'
    //     sh 'cat exposed'
    //   }
    // }

    stage ("Checking code with Synk") {
      steps {
        sh 'sudo apt-get install -y python3-pip'
        sh 'python3 -m venv venv_snyk'
        // craete another virtual environment to run snyk. This should prevent pip issues
        sh 'source venv_snyk/bin/activate'
        sh 'pip install -r requirements.txt'

        echo 'Testing for security issues...'
        snykSecurity(
          snykInstallation: 'Snyk',
          snykTokenId: 'snyk_apitoken',
          // place other parameters here
          failOnIssues: 'true',
          severity: 'medium'
        )
      }
    }

    // stage("Perform SCA with OWASP") {
    //   steps {
    //     dependencyCheck additionalArguments: ''' 
    //                 -o "./" 
    //                 -s "./"
    //                 -f "ALL" 
    //                 --prettyPrint''', odcInstallation: 'owasp'

    //             dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        
    //     sh 'cat dependency-check-report.xml'
    //     // Ran this before and I don't think it flagged anything.
    //   }
    // }
  }
}
