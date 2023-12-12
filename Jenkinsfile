pipeline {
    agent{
		node {
			label 'maven'
		}
	}

    stages {
        stage('Hello') {
            steps {
                git branch: 'main', url: 'https://github.com/RazaaAdnan/tweet-trend.git'
            }
        }
    }
}
