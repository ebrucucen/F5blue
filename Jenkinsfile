node {
   stage('Preparation') { 
      // Get some code from a GitHub repository
      git 'https://github.com/mcgonagle/F5blue.git'
   }
   stage('Testing') {
      //Run the tests
      sh "/usr/local/bin/ansible-lint F5file_blue.yml"
      sh "/usr/local/bin/ansible-review F5file_blue.yml"
   }
   stage('Build') {
       //Ansible Playbook
       ansiblePlaybook(
         colorized: true, 
         inventory: 'hosts.ini', 
         playbook: 'F5file_blue.yml', 
         sudoUser: null,
         extraVars: [
            username: 'admin',
            password: [value: 'adminadmin', hidden: true],
            hosts: 'bigip_hosts'
         ])
      //chatops slack message that ansible run has completed
      slackSend( 
         channel: '#general', 
         color: 'good', 
         message: 'F5file Build Ran Successfully', 
         teamDomain: 'uniopsteam', 
         token: 'zkMRYtEXCEG3Q2FlUsS2Hjjv'
         )
   }
}
