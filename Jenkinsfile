pipeline {

    agent any

    stages {
        stage('build & unit tests') {
            steps {

                    withMaven(maven: 'M3') {
                        sh 'mvn clean install'}


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
