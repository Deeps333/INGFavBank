pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/mybranch']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Deeps333/INGFavBank.git']]])
		}
	}
	stage ('Build')
	   
	    {steps{
                sh '/usr/share/maven/bin/mvn clean package -Dmaven.test.skip=true'
	    }    }
        stage ('Update the Version')
		{ steps {
                sh '/usr/share/maven/bin/mvn build-helper:parse-version versions:set -DnewVersion=\'${parsedVersion.majorVersion}.${parsedVersion.minorVersion}.${parsedVersion.nextIncrementalVersion}\' -DgenerateBackupPoms=false'
	        sh 'git add .'
                sh 'git commit -m "Updated pom" pom.xml'
                sh 'git push origin HEAD:mybranch'
                }       }
       
	}}
      
