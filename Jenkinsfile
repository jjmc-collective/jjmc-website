pipeline {
    agent any
    stages {
	stage ('build') {
	    steps{
		sh 'docker run --rm -it \
              -v $(pwd):/src \
              -v $(pwd)/public:/target \
              klakegg/hugo:0.62.2'
	    }
	}
	stage ('deploy') {
	    steps{
	    sshagent(credentials : ['www-deployment']) {
                    sh 'rsync -r "$WORKSPACE/public/" www-deployment@trashcloud.ch:/var/www/jjmc-website/public'
        }
	    }
	}

    }
}