node {

    stage(name: 'Git Checkout'){
        checkout scm
    }

    stage(name: 'Build Image'){
        docker.build("ambawatyuvaraj/argocd")
    }
    stage(name: 'Test Image'){
        sh 'echo Test Passed'
    }
    stage(name: 'Push Image'){
        docker.withRegistry('https://registry.hub.docker.com','dockherhub'){
            push("${env.BUILD_NUMBER}")
        }
    }
    stage(name: 'Trigger Update Manifest Job'){
        echo "triggered updatemanifest job"
        build job: 'updatemanifest', parameters: [string(name:'DOCKERTAG', value: env.BUILD_NUMBER)]
    }

}