# helm-gitlabrunner-monitoring

The helm chart to deploy different prometheus resources (blackbox-servicemonitor-alertmanager-rule) on various k8s namesapaces

The required role are specified on role-gitlabrunner.yml file regarding least priviledge principle.

1- Installation

1-1 Helm considerations

  The installation is done using helm. Change gitlabUrl, runnerRegistrationToken, clusterWideAccess, image, tags and protected values in values.yaml to your desired state.
  
1-2 Adjust roles for "default" SA

  After creation of gitlab-runner namespace, the default  SA (service account) will be created. Since this SA is utilized to deploy monitoring resources to k8s cluster namespaces, some extra role are added to it.

1-3 Run following command respectively, to have a gitlab-runner instance on K8S cluster and also it's registration with your gitlab instance:

  kubectl create ns gitlabrunner
  
  kubectl create -f role-gitlabrunner.yaml
  
  helm repo add gitlab https://charts.gitlab.io
  
  helm repo update
    
  helm upgrade --install gitlabrunner -n gitlabrunner -f values.yaml gitlab/gitlab-runner

After that you should see green status under Available specific runners part.
