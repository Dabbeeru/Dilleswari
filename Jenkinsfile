 node {
    stage 'Checkout'
    checkout scm
    stage 'Build Maven'
    wrap([$class: 'ConfigFileBuildWrapper', managedFiles: [[fileId: 'global-settings', targetLocation: '', variable: 'GLOBAL_SETTINGS']]]) {
        sh "echo {env.GLOBAL_SETTINGS}"
        sh "${tool 'mvn'}/bin/mvn clean install --settings ${env.GLOBAL_SETTINGS}"
    }
}
