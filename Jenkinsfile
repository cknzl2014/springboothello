node {
    stage('Checkout') {
        checkout scm
    }
    stage('Test') {
        echo "Hallo"
        echo "aha"
    }
    stage('Test2') {
        echo "Leute"
    }
    stage('Maven') {
        docker.image('maven:3.3.3-jdk-8').inside {
	    writeFile file: 'settings.xml', text: "<settings><localRepository>${pwd()}/.m2repo</localRepository><mirrors><mirror><id>nexus</id><url>http://nexus:5000</url><mirrorOf>*</mirrorOf></mirror></mirrors></settings>"
            sh 'mvn -B -s settings.xml clean install'
        }
    }
}
