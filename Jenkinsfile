pipeline {
  agent any
  stages {
      stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Secret Scanning') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/devopsadmin12/Demo-WebGoat.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
     
    stage ('SCA') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/devopsadmin12/Demo-WebGoat/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'sudo cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml || true'
        
      }
    }
 }
}
