pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/Deeps333/INGFavBank.git'
		}
	}
	stage ('Build')
	   
	    {steps{
                sh '/usr/share/maven/bin/mvn clean package -Dmaven.test.skip=true'
	    }    }
        stage ('Update the Version')
		{ steps {
                sh '/usr/share/maven/bin/mvn build-helper:parse-version versions:set -DnewVersion=\'${parsedVersion.majorVersion}.${parsedVersion.minorVersion}.${parsedVersion.nextIncrementalVersion}\' -DgenerateBackupPoms=false'
	        }       }
	}}
      
