pipeline {

    agent any

    stages {

        stage('build & unit tests') {

            steps {

                node(label:’build') {
                    withMaven(globalMavenSettingsConfig: 'maven-settings',jdk: 'jdk-8',maven: 'mvn-3.3.9') {
                        sh 'mvn clean install'}
                }

            }
        }

        stage('static analysis') {

            steps {

                node(label:’build') {

                    sleep(5)
                }

            }
        }

        stage('acceptance-tests') {

            steps {

                parallel (

                        chrome: { sleep(5) },
                        edge: { sleep(5) },
                        firefox: { sleep(5) }
                )


            }

        }


        stage('staging') {

            steps {
                node('any') {
                    sleep(5)
                }
            }

        }
        stage('manual-approval'){

            steps {
                input message: 'Déploiement en production?', ok:'Oui'
            }



        }
        stage('deploy'){

            steps {
                node('any') {
                    sleep(5)
                }
            }


        }


    }

}
