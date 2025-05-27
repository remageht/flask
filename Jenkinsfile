pipeline {
    agent any

    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select environment')
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying to ${params.ENV}"

                    // Очистка рабочей директории
                    cleanWs()

                    // Копирование файлов через SSH
                    sshPublisher(
                        publishers: [
                            sshPublisherDesc(
                                configName: 'server',
                                transfers: [
                                    transferSet(
                                        sourceFiles: '**/*',
                                        removePrefix: '',
                                        remoteDirectory: "/home/proger/app_${params.ENV}"
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}
