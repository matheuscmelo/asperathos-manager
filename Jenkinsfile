pipeline {
  agent any
  stages {
    stage('Unit') {
      steps {
        sh 'tox'
      }
    }
    stage('Integration') {
      steps {
        sh 'docker run -p 5000:5000 -v /.kube:/.kube -e KUBECONFIG="/.kube/config" 10.11.5.6:5000/asperathos-manager:1.0 &'
        sh 'docker run -p 5000:5000 -v /.kube:/.kube -e KUBECONFIG="/.kube/config" 10.11.5.6:5000/asperathos-controller:1.0 &'
        sh 'docker run -p 5000:5000 -v /.kube:/.kube -e KUBECONFIG="/.kube/config" 10.11.5.6:5000/asperathos-visualizer:1.0 &'
        sh 'docker run -p 5000:5000 -v /.kube:/.kube -e KUBECONFIG="/.kube/config" 10.11.5.6:5000/asperathos-monitor:1.0 &'
        sh 'git clone https://github.com/matheuscmelo/integration && cd integration && pip install -r requirements.txt && python run_tests.py'
      }
    }
  }
}
