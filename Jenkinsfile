pipeline {
   agent any
    options {
             skipDefaultCheckout true
	}
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
	        sh 'sudo git add .'
                sh 'sudo git commit -m "Updated pom" pom.xml'
                sh 'sudo git push https://Deeps333:Deepanshu333@github.com/Deeps333/INGFavBank.git HEAD:mybranch'
                }       }
            post { 
             always { 
            cleanWs()
        }
    }
       
	}}
      
