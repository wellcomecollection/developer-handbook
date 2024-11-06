# NodeJS updates for Auth0

When upgrades are required, Auth0 will send out emails warning us about it. It's on us to keep an eye out for those and implement the required changes, following the recommended versions of Node. It may be that those changes have to be done in multiple parts of the app.

## Extensibility
[Auth0 Documentation](https://auth0.com/docs/get-started/tenant-settings#extensibility)

We have staging and production tenants in Auth0 that are described in Terraform and can be updated independently. The node version for the whole tenant is _not_ terraformed, and is a manual change. The tenant level Node version impacts existing "custom database action scripts", and sets the default node version for _new "actions"_ (see the difference between "custom database action scripts" and "actions" below). **Existing actions are not upgraded and need doing on a per action basis**.

You may upgrade the Node version of the whole tenant by going into advanced settings, near the bottom is the Extensibility dropdown.

Upgrade the Node version in the staging tenant **first**, then test all the actions & custom database triggers, as well as sign in to `www-stage.wellcomecollection.org`. Then if that passes, do the same with the prod tenant.

The build process for our integration uses the Node version in the Identity [Dockerfile](https://github.com/wellcomecollection/identity/blob/main/.buildkite/Dockerfile#L1). If you're upgrading the Node version, you'll need to have a look at the [Buildkite pipeline script](https://github.com/wellcomecollection/identity/blob/main/.buildkite/pipeline.yml#L34) and determine a deployment strategy, which we've yet to do at this point.

Our "[actions](https://auth0.com/docs/customize/actions)" are documented in the [Identity repo](https://github.com/wellcomecollection/identity/tree/main/packages/apps/auth0-actions). You may consult them in the Auth0 tenant dashboard.

Our "[custom database action scripts](https://auth0.com/docs/authenticate/database-connections/custom-db/create-db-connection)" are also documented in [the Identity repo](https://github.com/wellcomecollection/identity/tree/main/packages/apps/auth0-database-scripts). You may consult them in the Auth0 tenant dashboard.

Both sets are concerned with keeping Sierra in sync with Auth0.

### Actions
The actions can be upgraded through the Auth0 dashboard in the Actions library. Should a new Node version be available, it'll flag it and allow you to upgrade and test your script. Once tested, you may deploy it. Our staging environment (`www-stage.wellcomecollection.org`) uses the Auth0 staging tenant, so you may test it there first.

Review logs (under monitoring -> logs) to confirm that sign-ins are behaving correctly in staging before moving on to prod. Then go ahead with the production tenant.

Terraformed actions [_can_ specify runtime version](https://registry.terraform.io/providers/auth0/auth0/latest/docs/resources/action#runtime) rather than use the global setting for the tenant. In the Identity configuration, [we don't](https://github.com/wellcomecollection/identity/blob/main/infra/scoped/auth0-actions.tf#L1) and therefore use the default - so also no code change required here, just a re-deployment.

### Custom database action scripts
You can test the database scripts changes in the Auth0 staging tenant (under Authentication -> Database -> Sierra-Connection -> Custom database), as well as on `www-stage.wellcomecollection.org`, depending on what needs testing. Once that's working, move on to prod updates.

Review logs (under monitoring -> logs) to confirm that sign-ins are behaving correctly in staging before moving on to prod.