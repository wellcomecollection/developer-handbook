---
description: List of useful things for an engineer who's just joined the team - Welcome!
---

# Onboarding

### Project Management Tool

We use [Github projects](https://github.com/orgs/wellcomecollection/projects) to show and communicate on what we are working on.

### Environments

1. Staging - [https://www-stage.wellcomecollection.org/](https://www-stage.wellcomecollection.org/)
2. Production - [https://wellcomecollection.org/](https://wellcomecollection.org/)
3. Preview of live without cloud front - [https://preview.wellcomecollection.org/opening-times](https://preview.wellcomecollection.org/opening-times)

### Dashboard

[Our dashboard](https://dash.wellcomecollection.org/) contains all useful links and services for WellcomeCollection, and serves for three reporting tools:

* [Prismic linting report](https://dash.wellcomecollection.org/prismic-linting/): This is for our Editorial team to be aware of various linting errors and warning in Prismic, our CMS. The script that is run is owned by us and more linting rules can be added by devs [in our codebase](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/prismic-model/lintPrismicData.ts).
* [pa11y report](https://dash.wellcomecollection.org/pa11y): [Pa11y](https://pa11y.org/) is a third party package that tests specified pages against WCAG standards. Find out more in [our README file](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/pa11y).
* Toggles: See [Toggles page](https://app.gitbook.com/s/7ftXlBv9uu465I0Z76rS/toggles-feature-flags).

### Code base

Pull down local version for development. Please check the readme file and start both services catalogue and content. The [repository](urls-on-wellcomecollection.org.md) has other services as well within the repository.

The application uses [Next.js](https://nextjs.org/) which is a React framework

#### Committing Code & Branching & Environments

When working on any new work, you will need to create a new feature branch from main.

Make sure you pull the latest main before branching.

Once the work has been implemented, tested, you can create a pull request and add the code owners to review the work for this to be approved.

Once code has been code reviewed and approved this can be merged into main.

Main branch will be automatically deployed to the staging environment if required to be viewed or approved via business. Deployment to prod can be done through [Buildkite](https://buildkite.com/wellcomecollection) afterwards - ask a colleague  to help for the first time you do it and they can give you more details.

### Api

The platform calls three core API's, which Wellcome collection uses.

1.  **Catalogue** - WellcomeTrust own api

    Repository : [https://github.com/wellcomecollection/catalogue](https://github.com/wellcomecollection/catalogue)

    Documentation to api : [https://developers.wellcomecollection.org/](https://developers.wellcomecollection.org/)
2. **Content** - Our API to consume and transform Prismic Content\
   Repository: [https://github.com/wellcomecollection/content-api](https://github.com/wellcomecollection/content-api)
3.  **Prismic -** provide dynamic content for various pages using Prismic

    [Area where we make calls to WellcomeCollection Prismic API](https://github.com/wellcomecollection/wellcomecollection.org/tree/master/common/services/prismic)

    Before playing around with Prismic api please read docs

    [https://prismic.io/docs/rest-api/basics/the-api-browser](https://prismic.io/docs/rest-api/basics/the-api-browser)

### More about Prismic

#### [**API documentation**](https://prismic.io/docs/setup-vanilla-javascript)

#### **API requests**

Prismic have [their own api interface](https://wellcomecollection.prismic.io/api) which you can request of Wellcome collection content

#### **Preview edited content**

[Ability to preview Prismic content](https://prismic.io/docs/rest-api/beyond-the-api/the-preview-feature)

Content editors can see preview content of dynamic pages. Caching has been disabled (cloudfront) within this domain: [https://preview.wellcomecollection.org](https://preview.wellcomecollection.org).

Previewing content only works on page level, so having custom types may not return back. You will need to publish the content.

#### **Development**

You should be able to view preview locally, a cookie is set locally which allows to view content locally.

The preview button should link you to [localhost:3000](http://localhost:3000)

### Logs

1. You should be able to view logs of the live server using kibana
2. Sentry also provides front end issues and logs

### Dev Ops

#### **CI Pipeline**

We use buildkite to deal with our Pipeline build chain for continuous integration

You should be able to view various pipelines for all the applications and the builds such as

* catalogue front end
* catalogue api

[https://buildkite.com/wellcomecollection](https://buildkite.com/wellcomecollection)

#### P**ipeline settings**

[https://github.com/wellcomecollection/wellcomecollection.org/blob/master/.buildkite/pipeline.yml](https://github.com/wellcomecollection/wellcomecollection.org/blob/master/.buildkite/pipeline.yml)

**AWS**

#### **Terraform**

Most of the applications uses terraform which we use provider AWS - allows automate, managing provisioning infrastructure by code.

Catalogue Application of Terraform code

[https://github.com/wellcomecollection/wellcomecollection.org/tree/master/catalogue/terraform](https://github.com/wellcomecollection/wellcomecollection.org/tree/master/catalogue/terraform)

Useful videos explaining the purpose of Terraform and purpose of use for Dev ops responsibilities.

{% embed url="https://www.youtube.com/watch?v=HmxkYNv1ksg" %}

{% embed url="https://www.youtube.com/watch?v=l5k1ai_GBDE" %}
