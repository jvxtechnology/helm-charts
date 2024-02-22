This is a slightly customized version of the bitnami Odoo chart. It adds a github secret and an initContainer which is responsible for pulling one or more github repos.

After installing this chart, you must perform the following steps to get SafeInquire working:

1. Apps -> Activate Discuss module
2. Settings -> Activate Developer Mode
3. Apps -> Update Apps List
4. Active the following modules:
  - safeInquire
  - jvx-desk-debranded-email-templates
  - jvx-desk-hide-activities
  - jvx-desk-hide-app-switcher
  - jvxtechnology/jvx-desk-hide-discuss
  - jvx-desk-ui-skin-beige-alert
  - softhealer-odoo-backend-debranding
  - softhealer-odoo-base-debranding

**Troubleshooting**
If the primary container fails to deploy with a generic error ("Back-off restarting failed container si-safeinquire"), the problem is very likely to be that the github repo(s) cannot be accessed. Ensure that you've provided either a githubToken or an existing secret. Also, ensure that the token is valid by attemptinga manual clone of each repo using the same personal access token. The command to clone a git repo using a specific token is:

  git clone https://<github token>@github.com/jvxtechnology.com/<repo>


Another common issue is that you're trying to redeploy when a previous installation pvc's still remains. The primary odoo data pvc is not deleted during a chart uninstall. It must be manually deleted. Without special accomodation, new chart deployments will fail while the old PVC is in place.
