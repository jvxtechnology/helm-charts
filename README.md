## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

  helm repo add jvx https://jvxtechnology.github.io/helm-charts/

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
<alias>` to see the charts.

To install the <chart-name> chart:

    helm install my-<chart-name> <alias>/<chart-name>

To uninstall the chart:

    helm delete my-<chart-name>

To obtain mysql passwords:
  MariaDB root password:
    kubectl -n <namespace> get secret <release name>-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 --decode; echo
  
  GLPI db username:
    kubectl -n <namespace> get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-user}" | base64 --decode; echo
  
  GLPI db password:
    kubectl -n <namespace> get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-password}" | base64 --decode; echo


## Development

  This repo uses a github action to auto-deploy new chart versions. To cause a new version to be published, increase the chart version in Chart.yaml, commit, and push. It can take a few minutes for this process to complete. You can check progress by browsing to this repo on github.com and consulting the 'Actions' pane.
