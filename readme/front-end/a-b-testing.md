---
description: >-
  A/B tests can be created using special variants of the <a
  href="https://app.gitbook.com/o/-LumfFcEMKx4gYXKAZTQ/s/DPDDj27NI2F2kPukWrC1/~/changes/75/readme/front-end/toggles-feature-flags">toggles</a>
---

# A/B testing

### Steps to create an A/B test

* Add a test object to [`toggler.ts`](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/cache/edge_lambdas/src/toggler.ts) and add an equivalent test object with the same `id` to [`toggles.ts`](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/webapp/toggles.ts) :

```
{
  id: 'someToggleId',
  title: 'New subject tags on works pages',
  range: [0, SOME_PERCENTAGE],
  when: request => {
    return !!request.uri.match(/SOME_REGEX/);
  },
}
```

* Update and upload the lambda deployment package:

```
docker compose build edge_lambdas
AWS_PROFILE=experience-developer docker compose run edge_lambdas yarn deploy
```

* deploy the lambda:

```
terraform plan -out=terraform.plan
terraform apply terraform.plan
```

* Check `www-stage` and verify the test cookie (`toggle_someToggleId`) is set.
* Check the data is being sent to GA (either `someToggleId` or `!someToggleId`). You should initially be able to see the toggles dataLayer variable being set (`DLV - Toggles`) in GTM, then this data should get sent to GA as a custom dimension (note you might not be able to see this until the next day).
* Update `locals.tf` with values from previous terraform and re-run the terraform steps above to get the changes in to production
