# NodeJS updates for Auth0

When upgrades are required, Auth0 will send out emails warning us about it. It's on us to keep an eye out for those and implement the required changes, following the recommended versions of Node. It may be that those changes have to be done in multiple parts of the app.

In our case, this has recently meant two parts:

## Extensibility
[Auth0 Documentation](https://auth0.com/docs/get-started/tenant-settings#extensibility)

We have staging and production tenants in Auth0 that are described in Terraform and can be updated independently. The node version for the whole tenant is _not_ terraformed, and is a manual change. The Identity repository, though, _does_ use Terraform workspaces.

You may upgrade the Node version of the whole tenant by going into [advanced setting](https://manage.auth0.com/dashboard/eu/wellcomecollection/tenant/advanced), near the bottom is the Extensibility dropdown.
We'd encourage upgrading the Node version in the staging tenant first, then test all the actions & custom database triggers, as well as sign in to `www-stage.wellcomecollection.org`. Then if that passes, do the same with the prod tenant.

The build process for these integration being set differently, you'll need to make changes in the Identity repo. You may consult the Node version in the identity [Dockerfile](https://github.com/wellcomecollection/identity/blob/main/.buildkite/Dockerfile#L1) or have a look at the [Buildkite pipeline script](https://github.com/wellcomecollection/identity/blob/main/.buildkite/pipeline.yml#L34).


## Custom actions
The tenant level Node version (upgraded above) impacts existing "custom database action scripts", and sets the default node version for _new "actions"_ (see the difference between "custom database action scripts" and "actions" below). **Existing actions are not upgraded and need doing on a per action basis**.

Our "[actions](https://auth0.com/docs/customize/actions)" are documented in the [Identity repo](https://github.com/wellcomecollection/identity/tree/main/packages/apps/auth0-actions). You may consult them [in the Auth0 dashboard](https://manage.auth0.com/dashboard/eu/wellcomecollection-stage/actions/library).

Our "[custom database action scripts](https://auth0.com/docs/authenticate/database-connections/custom-db/create-db-connection)" are also documented in [the Identity repo](https://github.com/wellcomecollection/identity/tree/main/packages/apps/auth0-database-scripts). You may consult them [in the Auth0 dashboard](https://manage.auth0.com/dashboard/eu/wellcomecollection-stage/connections/database/con_x8EvHgL6VO1QNYzn/plug).

Both sets are concerned with keeping Sierra in sync with Auth0.

### Actions
The actions can be upgraded and tested in the staging environment (`www-stage`), and that change can then be deployed in both the staging and prod tenants.
Although in this case, actions can specify runtime version (rather than use the global setting for the tenant), we _don't_ in the Identity configuration and the default is used - so also no code change required here, just a re-deployment.

### Custom database action scripts
You can test the database scripts changes in the staging environment as well before deploying to prod inside the Auth0 dashboard. It lets you test the functions with some username and password, or whatever input it expects.

In both cases, [review logs in a tenant](https://manage.auth0.com/dashboard/eu/wellcomecollection/logs) (under monitoring -> logs) to see that sign-ins are behaving correctly in staging before moving on to prod.