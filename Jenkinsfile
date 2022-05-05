podTemplate(yaml: '''
  apiVersion: v1
  kind: Pod
  spec:
    containers:
    - name: centos
      image: centos
      command:
      - sleep
      args:
      - 99d
    restartPolicy: Never
''') {
  node(POD_LABEL) {
    stage('k8s') {
      git 'https://github.com/kavinasi/Week9Exer1.git'
      container('centos') {
        stage('start calculator') {
          sh '''
          curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
          chmod +x ./kubectl
          ./kubectl apply -f calculator.yaml -n staging
          ./kubectl apply -f hazelcast.yaml -n staging
          '''
        }
      }
    }
  }
}
