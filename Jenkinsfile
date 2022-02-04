properties([
  parameters([
    // choice(choices: envs, description: '', name: 'Env'),
    [
      $class: 'ChoiceParameter', 
      choiceType: 'PT_SINGLE_SELECT', 
      description: '*cluster', 
      filterLength: 1, 
      filterable: false, 
      name: 'cluster',  
      script: [
        $class: 'GroovyScript', 
        fallbackScript: [
          classpath: [], 
          sandbox: true, 
          script: 'return["error"]'
        ], 
        script: [
          classpath: [], 
          sandbox: true, 
          script: 'return["go","us01"]'
        ]
      ]
    ], 
    [
      $class: 'CascadeChoiceParameter', 
      choiceType: 'PT_CHECKBOX', 
      description: '*region(support multi-choice)', 
      filterLength: 1, 
      filterable: false, 
      name: 'region', 
      referencedParameters: 'cluster', 
      script: [
        $class: 'GroovyScript', 
        fallbackScript: [
          classpath: [], 
          sandbox: true, 
          script: 'return["error"]'
        ], 
        script: [
          classpath: [], 
          sandbox: true, 
          script: '''
          if (cluster.equals("go")){
            return[
              "sj-blue",
              "sj-green"
            ]
          }else if (cluster.equals("us01")) {
            return[
              "sj-blue",
              "sj-green",
              "dv-blue",
              "dv-green"
            ]
          }'''
        ]
      ]
    ],
    [
      $class: 'ChoiceParameter', 
      choiceType: 'PT_SINGLE_SELECT', 
      description: '*catagory', 
      filterLength: 1, 
      filterable: false, 
      name: 'catagory',  
      script: [
        $class: 'GroovyScript', 
        fallbackScript: [
          classpath: [], 
          sandbox: true, 
          script: 'return["error"]'
        ], 
        script: [
          classpath: [], 
          sandbox: true, 
          script: 'return["sipzone", "pbx-others", "host-init", "redis"]'
        ]
      ]
    ], 
    [
      $class: 'CascadeChoiceParameter', 
      choiceType: 'PT_CHECKBOX', 
      description: '*application', 
      filterLength: 1, 
      filterable: false, 
      name: 'application', 
      referencedParameters: 'catagory', 
      script: [
        $class: 'GroovyScript',
        fallbackScript: [
          classpath: [],
          sandbox: true, 
          script: 'return["error"]'
          ], 
          script: [
            classpath: [], 
            sandbox: true, 
            script: '''
            if (catagory.equals("sipzone")){
              return[
                "csms-agent",
                "pbx-freeswitch",
                "pbx-opensips",
                "pbxms",
                "pbx-rs",
                "pbx-rtts",
                "pbx-etcd",
                "pbx-wss",
                "pbx-routeengine",
                "pbx-routedatasync",
                "pbx-routeopensips",
                "aisense",
                "aisense-nginx",
                "verify-app-health",
                "verify-image-tags",
                "keepalived-alerts"
              ]
            }else if (catagory.equals("pbx-others")) {            
              return[
                "coredump",
                "filebeat",
                "filebeat-sbc",
                "flask-proxy-sbc",
                "fs-failover-alarm",
                "packetbeat",
                "pbx-metrics",                                  
                "pbx-watcher",
                "pbxms_exporter",
                "s3_deploy",
                "telegraf-sbc",
                "telegraf-server",
                "zabbix_agent",
                "zagent",
                "keepalived",
                "pbx-wsskeepalived",
                "pbx-routekeepalived"
              ]
            }else if (catagory.equals("host-init")) {                          
              return[
                "all",
                "docker-init",
                "ansible-venv",
                "cadvisor",
                "node-exporter",
                "twistlock-defender",
                "stunnel"              
              ]              
            }else if (catagory.equals("redis")) {    
              return[     
                "redis_node_install",
                "redis_cluster_install",
                "redis_cluster_uninstall",
                "redis_export_install",
                "redis_checkConf"
              ]
            }'''
          ]
        ]
    ], 
    [
      $class: 'CascadeChoiceParameter', 
      choiceType: 'PT_SINGLE_SELECT', 
      description: 'optional', 
      filterLength: 1, 
      filterable: false, 
      name: 'tag', 
      referencedParameters: 'application', 
      script: [
        $class: 'GroovyScript', 
        fallbackScript: [
          classpath: [], 
          sandbox: true, 
          script: 'return["error"]'
         ], 
          script: [
            classpath: [], 
            sandbox: true, 
            script: '''
            if(application.equals("csms-agent")){
              return[
                "add-fs-path",
                "add-ms-path",
                "add-opensips-path",
                "add-rs-path",
                "add-rtts-path",
                "add-routeengine-path"
              ]
            }else if (application.equals("pbx-freeswitch")){
              return[
                "",
                "update-conf",
                "restart_container",
                "pull-image",
                "check-version"
              ]
            } else if(application.equals("pbx-opensips")){
              return[
                "",
                "update-conf",
                "update-db",
                "restart_container",
                "check-version",
                "install_keepalived"
              ]
            }else if(application.equals("pbxms")){
              return[
                "",
                "hotpatch",
                "check-version"
              ]
            } else if (application.equals("pbx-rs")) {
              return[
                "",
                "update-conf",
                "restart_container",
                "pull-image",
                "check-version",
                "remove-recording"
              ]
            } else if (application.equals("pbx-rtts")) {
              return[
                "",
                "update-conf",
                "restart_container",
                "pull-image",
                "check-version"
              ]
            } else if (application.equals("zagent")) {
              return[
                "",
                "update",
                "stop",
                "remove"
              ]  
            }else if(application.equals("pbx-etcd")){
              return[
                "deployOnly,common,addActiveIp",
                "addMember,common,addActiveIp",
                "addActiveIp"
              ]
            }else if(application.equals("filebeat")){
              return[
                "filebeat_update",
                "troubleshooting_update",
                "fraud_update",
                "filebeat_cmdb",
                "filebeat_sbc_sys",
                "filebeat_sbc_trc"
              ]
            }else if(application.equals("filebeat-sbc")){
              return[
                "filebeat_sbc_act",
                "filebeat_sbc_aud",
                "filebeat_sbc_dbg",
                "filebeat_sbc_sys",
                "filebeat_sbc_trc"
              ]
            }else if(application.equals("packetbeat")){
              return[
                ""
              ]
            }else if(application.equals("zabbix_agent")){
              return[
                "opensips-deploy",
                "fs-deploy",
                "sipsak-deploy"
              ]
            }else if(application.equals("coredump")){
              return[
                "freeswitch",
                "opensips"
              ]
            }else if(application.equals("redis_cluster_install")){
              return[
                "cluster_install",
                "checkConf"
              ]
            }else if(application.equals("aisense-nginx")){
              return[
                "install_nginx",
                "install_keepalived"
              ]
            }else if(application.equals("aisense")){
              return[
                ""
              ]
            }else if(application.equals("pbx-wss")){
              return[
                "install_wss",
                "install_keepalived"
              ]
            }else if(application.equals("pbx-routeopensips")){
              return[
                "install_routeopensips",
                "install_keepalived"
              ]              
            } else if (application.startsWith("flask-proxy")) {
              return [
                "deploy",
                "remove"
              ]
            } else if (application.startsWith("telegraf")) {
              return [
                "deploy",
                "remove"
              ]
            } else if (application.startsWith("keepalived-alerts")) {
                return [
                    "enable",
                    "disable"
              ]  
            }else {
              return[
                ""
              ]
            }'''
          ]
        ]
      ], 
    [
      $class: 'CascadeChoiceParameter', 
      choiceType: 'PT_CHECKBOX', 
      description: 'optional', 
      filterLength: 1, 
      filterable: false, 
      name: 'label',
      referencedParameters: 'application',
      script: [
        $class: 'GroovyScript',
        fallbackScript: [
          classpath: [],
          sandbox: true, 
          script: 'return["error"]'
          ], 
          script: [
            classpath: [], 
            sandbox: true, 
            script: '''
            if (application.equals("csms-agent")){
              return[
                "pbx-freeswitch",
                "pbx-opensips",
                "pbxms",
                "pbx-rs",
                "pbx_rtts",
                "pbx-routeengine"
              ]
            } else if (application.equals("pbx-freeswitch")){
              return[
                "pbx-freeswitch"
              ]
            } else if (application.equals("pbx-opensips")){
              return[
                "pbx-opensips"
              ]
            } else if (application.startsWith("pbxms")){
              return[
                "pbxms"
              ]
            } else if (application.equals("pbx-rs")) {
              return[
                "pbx-rs"
              ]
            } else if (application.equals("pbx-rtts")) {
              return[
                "pbx_rtts"
              ]
            }else if (application.equals("pbx-etcd")){
              return[
                "pbx-etcd"
              ]
            }else if (application.equals("aisense-nginx")){
              return[
                "aisense-nginx"
              ]
            }else if (application.equals("aisense")){
              return[
                "aisense"
              ]
            }else if (application.equals("pbx-wss")){
              return[
                "pbx_wss"
              ]
            }else if (application.equals("pbx-routeopensips")){
              return[
                "pbx-routeopensips"
              ]              
            }else if (application.equals("pbx-routeengine") || application.equals("pbx-routedatasync") ){
              return[
                "pbx-routeengine"
              ]   
            }else if (application.equals("filebeat")){
              return[
                "pbx-freeswitch",
                "pbx-opensips",
                "pbxms",
                "pbx-rs",
                "pbx_rtts",
                "pbx_wss",
                "pbx-routeengine",
                "pbx-routeopensips"
              ]
            }else if (application.equals("filebeat-sbc")){
              return[
                "sbc-act",
                "sbc-aud",
                "sbc-dbg",
                "sbc-sys",
                "sbc-trc"
              ]
            }else if (application.equals("packetbeat")){
              return[
                "pbx-freeswitch",
                "pbx-opensips"
              ]
            }else if (application.equals("coredump")){
              return[
                "freeswitch",
                "opensips"
              ]
            }else if (application.equals("pbx-watcher")){
              return[
                "aisense-nginx",
                "pbx-opensips",
                "pbx-routeopensips",
                "pbx_wss"
              ]
            }else if (application.equals("keepalived-alerts")){
              return[
                "aisense-nginx",
                "pbx-opensips",
                "pbx-routeopensips",
                "pbx_wss"
              ]                  
            }else if (application.startsWith("telegraf") || application.startsWith("flask-proxy")) {
              return [
                "telegraf_sbc",
                "telegraf_server"
              ]                                                                        
            }else if (application.startsWith("redis") ) {    
              return[
                "pbx-redis",
                "redis_exporter_hosts"
              ]              
            } else {        
              return[
                  "pbx-freeswitch",
                  "pbx-opensips",
                  "pbxms",
                  "pbx-etcd",
                  "pbx-rs",
                  "pbx_rtts",
                  "pbx_wss",
                  "pbx-routeengine",
                  "pbx-routeopensips",
                  "aisense",
                  "aisense-nginx"
              ]
            }
            '''
           ]
        ]
     ], 
     string(name: 'limitHosts', defaultValue: '', description: 'Comma-separated IP list (optional)', trim: true),
     booleanParam(name: 'virtualenv', defaultValue: true, description: 'Use virtualenv for ansible python interpeter.'),
     booleanParam(name: 'mitogen', defaultValue: true, description: 'Use mitogen plugin.'),
     booleanParam(name: 'colorOutput', defaultValue: true, description: 'Enable color output text.'),     
     choice(name: 'verbose', choices: ['', '-vvv', '-vvvv'], description: 'Enable verbose logging.')
  ])
])


def runParallel = true
def buildStages
node {
  stage("deleteDir") {
      script{
          deleteDir()
          currentBuild.description = "[${params.cluster}] ${params.region} :: ${params.application}"
        }
    }
  stage('checkout') {
    checkout scm
  }  
  stage('Build and Deploy') {
    buildStages = prepareBuildStages()
    println("Build and Deploy.")
  }
  for (builds in buildStages) {
      parallel(builds)
      println("Deploy builds.")
  }
  stage('verification') {
      verificateStages = prepareVerificateStages()
      println("verification.")
  }
  for (verifications in verificateStages) {
      parallel(verifications)
  }
}

// Create List of build stages
def prepareBuildStages() {
  def buildStagesList = []
  def buildParallelMap = [:]
  def item=params.region.split(',')
  for (int i = 0; i < item.size(); ++i){
    def n = item[i]
    def item2=params.application.split(',')
    for (int j = 0;j<item2.size(); ++j){
      def m = item2[j]
      buildParallelMap.put((n+"-"+m), prepareOneBuildStage(n,m))
    }
   }
   buildStagesList.add(buildParallelMap)
  return buildStagesList
}

def prepareOneBuildStage(String region,String application) {
    return {
        stage("Build stage:${region} ${application}") {
            script{
                def command = "ansible-playbook -i env/${params.cluster}/${region}/hosts ${application}.yml -u jenkins --diff --vault-password-file /opt/jenkins/.vault/zcc-host-mgmt-201222"
                if ( params.mitogen == true ) {
                    command = "export ANSIBLE_CONFIG='./ansible-mitogen.cfg' && ${command}"
                }
                if ( params.colorOutput == true ) {
                    command = "export ANSIBLE_FORCE_COLOR=true && ${command}" 
                }                
                if ( params.tag != "" ) {
                    command = "${command} -t ${params.tag}"
                }
                if ( params.label != "" ) {
                    command = "${command} -l ${params.label}"
                }
                if ( params.limitHosts != "" ) {
                    command = "${command} --limit ${params.limitHosts}"
                }
                if ( params.virtualenv == true ) {
                    command = "${command} -e 'ansible_python_interpreter=/opt/venvs/ansible/bin/python'"
                }
                if ( params.verbose != "" ) {
                    command = "${command} ${params.verbose}"
                }
                sh(command)
            }
        }
    }
}

def prepareVerificateStages() {
  def verificateStagesList = []
  def verificateParallelMap = [:]
  def item=params.region.split(',')
  for (int i = 0; i < item.size(); ++i){
    def n = item[i]
    def item2=params.application.split(',')
    for (int j = 0;j<item2.size(); ++j){
      def m = item2[j]
      verificateParallelMap.put((n+"-"+m), prepareOneVerificateStage(n,m))
    }
   }
   verificateStagesList.add(verificateParallelMap)
  return verificateStagesList
}

def prepareOneVerificateStage(String region,String application) {
  return {
    stage("verification stage:${region} ${application}") {
            script{
              def command = "ansible -i env/${params.cluster}/${region}/hosts"
              def otherContainerApps = ["pbx-etcd","keepalived","filebeat","packetbeat","pbxms_exporter"]
              if ( "${application}"=="pbx-freeswitch" ){
                sh("${command} ${application} -m shell -a 'netstat -nap |grep 5060' -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbxfs' -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'grep START_PYTHON.*False /opt/docker/freeswitch/conf/zoom_global_def.py || ps -ef|grep -v grep|grep zoom_main.py' -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'ps -ef|grep -v grep|grep zoom_main.py|wc -l' -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-rs" ) {
                sh("${command} ${application} -m shell -a 'netstat -nap |grep 5060'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbxrs'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'ps -ef|grep -v grep|grep zoom_main.py'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'ps -ef|grep -v grep|grep zoom_main.py|wc -l '  -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-rtts" ) {
                sh("${command} ${application} -m shell -a 'netstat -nap |grep 5060'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbxrtts'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'ps -ef|grep -v grep|grep streamworker'  -u jenkins --diff -b ")
                sh("${command} ${application} -m shell -a 'ps -ef|grep -v grep|grep streamworker|wc -l '  -u jenkins --diff -b ")                
              } else if ( "${application}"=="pbx-opensips" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i opensips' -u jenkins --diff -b || true ")
                sh("${command} ${application} -m shell -a 'ip a|grep /32' -u jenkins --diff -b || true")
              } else if ( "${application}"=="pbxms" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i docker_pbx_microservice' -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-etcd" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i etcd' -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-wss" ){
                sh("${command} ${params.label} -m shell -a 'docker ps|grep -i pbx_wss'  -u jenkins --diff -b ")  
                sh("${command} ${params.label} -m shell -a 'ip a|grep /32' -u jenkins --diff -b || true")    
              } else if ( "${application}"=="aisense" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i docker_pbx_aisense'  -u jenkins --diff -b ")                  
              } else if ( "${application}"=="aisense-nginx" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i docker_pbx_aisense_nginx'  -u jenkins --diff -b ")  
                sh("${command} ${application} -m shell -a 'ip a|grep /32' -u jenkins --diff -b || true")                      
              } else if ( "${application}"=="pbx-routedatasync" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbx_routedatasync'  -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-routeengine" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbx_routeengine'  -u jenkins --diff -b ")
              } else if ( "${application}"=="pbx-routeopensips" ){
                sh("${command} ${application} -m shell -a 'docker ps|grep -i pbx_routeopensips' -u jenkins --diff -b || true ")
                sh("${command} ${application} -m shell -a 'ip a|grep /32' -u jenkins --diff -b || true")                                            
              } else if ( "${application}"=="pbx-watcher" ){
                sh("${command} ${params.label} -m shell -a 'docker ps|grep -i watcher' -u jenkins --diff -b ")
              } else if ( "${application}"=="filebeat-sbc" ){
                sh("${command} ${params.label} -m shell -a 'docker ps|grep -i filebeat_sbc' -u jenkins --diff -b ")
              } else if ( otherContainerApps.contains(application) ){
                sh("${command} ${params.label} -m shell -a 'docker ps|grep -i ${application}'  -u jenkins --diff -b || true")
              } else {
                println("This stage has no steps")
              }
            }
      }
  }
}