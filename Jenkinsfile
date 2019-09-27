timestamps {

node () {

    stage ('triggerJob - Checkout') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], git poll: true, userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/alamscode/shared-library-jenkins']]]) 
    }
    
    stage ('triggerJob - Build') {
        sh """ 
        echo "committed to shared library" 
        """ 
    }
        
    stage ('post-builds-parallel')  {  
        parallel build1: {
                        stage ('post-build') {
                            build job: 'sharedLibraryJob/master'
                        }
                    },
                build2: {
                        stage ('post-build') {
                            build job: 'sharedLibraryJob/dev'
                            }
                }            
        }
    }
}

