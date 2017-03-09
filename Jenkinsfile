pipeline {

    agent any

    stages {

        stage('build & unit tests') {

            steps {

                node('build') {

                    withMaven(globalMavenSettingsConfig: 'maven-settings',
                            jdk: 'jdk-8',
                            maven: 'mvn-3.3.9') {
                        sh 'mvn clean install'
                    }


                    sleep(5)
                }

            }
        }

        stage('static analysis') {

            steps {

                node('build') {

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
                node {
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
                node {
                    sleep(5)
                }
            }


        }


    }

}