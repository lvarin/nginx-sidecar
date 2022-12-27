# Nginx sidecar

This repository is used in the article [Reverse proxy authentication using a sidecar container](http://docs.csc.fi/cloud/rahti/tutorials/sidecar_proxy_authentication/). It contains the files needed to create the [nginx sidecar](https://hub.docker.com/repository/docker/lvarin/nginx-sidecar) image, and the template yaml files that define the application.

## Quick start

Edit the file `templates/filebeat-cm.yml` and fill up the project number in the `project_name' field

```sh
oc create -f templates/filebeat-cm.yml
oc create -f templates/DeploymentConfig.yaml
oc create -f templates/Service.yaml
oc create route edge sidecar --service=nginx-okd  --insecure-policy='Redirect'
oc get route sidecar
```

Log in [Koivu](https://koivu.wood.csc.fi/) and select the same project that you filled up. You will see the log entries from the `nginx` container you set up in `templates/DeploymentConfig.yaml`. Any furher development, you may check <https://wiki.csc.fi/Observability/Logging/UserGettingStarted>.

