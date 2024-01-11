### Overview ###

JVX Helpdesk application based on GLPI.


### GLPI SETUP ###

SQL_SERVER: <release-name>-mariadb

## Get auto-generated secrets
## Be sure to add a namespace, if needed
# GLPI user/password
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-user}" | base64 --decode; echo
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-password}" | base64 --decode; echo

# Mariadb Root
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 --decode; echo

Select DB: glpi
