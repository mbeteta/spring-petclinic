pipeline {


    tools{
        maven 'mvn-3.3.9'
        jdk 'jdk-8'
    }

    stage('build & unit tests') {

        node('build') {

            steps {
                withMaven(globalMavenSettingsConfig: 'maven-settings',
                    jdk: 'jdk-8',
                    maven: 'mvn-3.3.9') {
sh 'mvn clean install'
                }

            }


            sleep(5)
        }
    }

    stage('static analysis') {

        node('build') {

            sleep(5)
        }
    }

    stage('acceptance-tests') {

        parallel (

                chrome: { sleep(5) },
                edge: { sleep(5) },
                firefox: { sleep(5) }
        )
        input message: 'Déploiement en production?', ok:'Oui'

    }


    stage('staging') {

        node {
            sleep(5)
        }

    }
    stage('manual-approval'){

        node {
            sleep(5)
        }

    }
    stage('deploy'){

        node {
            sleep(5)
        }

    }
}