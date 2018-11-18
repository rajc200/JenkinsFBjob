pipeline { 

	agent any
	
	parameters {
        choice(
            // choices are a string of newline separated values
            // https://issues.jenkins-ci.org/browse/JENKINS-41180
            choices: 'a\nb\nc\nd\ne',
            description: '',
            name: 'var')
    }
  stages {
	stage("\u2777 build") {
			when {
			expression { params.var =~ 'A|a' }
				}
			steps {
			echo " Sat May 19 06:41:57 UTC 2018"
			echo "${params.var} iii"
    		}
	}

	stage("\u2776 build_olds") {
			agent { label "node02" }
			when {
			expression { params.var =~ 'A|a' }
				}
			steps {
			sh '''sudo mkdir /home/sam/sap -p '''
			echo "${params.var} iii"
    		}
	}


	stage("build_new") {
			agent { label "node02" }
			when {
			expression { params.var =~ 'A|a' }
				}
			steps {
			sh '''sudo mkdir /home/sam/sap/sare -p '''
			echo "${params.var} iii"
    		}
	}


 }

}
