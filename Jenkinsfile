pipeline {
    agent any
        parameters {
            choice(
                name: 'tfstate',
                choices:"planned\npresent\nabsent",
                description: "Choose appropriate!")
            string(
                name: 'tfplan',
                defaultValue:"$WORKSPACE/flusx7/aws/aws.tfplan",
                description: "Path of the plan file")
            string(
                name: 'projectpath',
                defaultValue:"$WORKSPACE/flusx7/aws",
                description: "Project Path")
    }
    stages {
        stage("build") {
            steps {
          sh('echo Initiating playbook')

          sh('ls -ltr ${WORKSPACE}')

          wrap([$class:'AnsiColorBuildWrapper', 'colorMapName': 'XTerm']) {

            sh "export ANSIBLE_FORCE_COLOR=true; "

               ansiblePlaybook(

                 installation: 'Ansible2.7.1',

                 limit: 'localhost',

                 become: 'true',

                 playbook: 'flux7/terraform.tml',

                 colorized: 'true',

                 tags: 'tfstart',

                 extras: '-e projectpath=${projectpath} -e tfstate=${tfstate} -e tfplan=${tfplan} -vvv'

               )

          }

       }
        }
    }
}