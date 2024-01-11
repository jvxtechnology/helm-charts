### Overview ###

JVX Helpdesk application based on GLPI.


### GLPI SETUP ###

## Get auto-generated secrets
## Be sure to add a namespace, if needed
# GLPI user/password
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-user}" | base64 --decode; echo
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-glpi-password}" | base64 --decode; echo

# Mariadb Root
kubectl get secret gdesk-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 --decode; echo

## Configure GLPI database
SQL Server: <release-name>-mariadb
GLPI user credentials: <from above>
Select DB: glpi

Default login is glpi/glpi

*Note that the glpi container may need to be restarted after initializing the db in order for install/install.php to be deleted:
  kubectl rollout restart deployment/<deployment-name>-glpi

**Currently, you must enable timezones by running the following commands:
# In the mariadb container (root password required)
mariadb-tzinfo-to-sql /usr/share/zoneinfo | mariadb -u root -p mysql
mariadb -u root -p mysql -e 'GRANT SELECT ON `mysql`.`time_zone_name` TO 'fN2ssIdN';'
mariadb -u root -p mysql -e 'FLUSH PRIVILEGES;'

# In the GLPI container
php bin/console database:enable_timezones
