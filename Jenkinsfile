pipeline {
agent any
stages{
stage('Build') {
	steps {
	echo 'Building..'
        sh 'mvn install -DskipTests'     	
}
}
stage('Test') {
	steps {
	echo 'Testing..'
}
}
stage('Deploy'){
	steps {
	echo 'Deploying...'
	}
}
}
}
