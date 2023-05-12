---
description: URLs, redirects, marketing redirects (vanity URLs)
---

# URLs on wellcomecollection.org

## Current status (as of March 2020)

Currently, we mint a URI at source, e.g. in Prismic, REST API.

This is the canonical URL.

For those pages where we need a more human readable URL, these need to be set up as a 3xx redirect.

Full redirect list [https://github.com/wellcomecollection/wellcomecollection.org/blob/d4e346c20abb8e9228980bd11639c881d6f96551/cache/edge\_lambdas/redirects.js](https://github.com/wellcomecollection/wellcomecollection.org/blob/d4e346c20abb8e9228980bd11639c881d6f96551/cache/edge\_lambdas/redirects.js)

Questions: Redirects put in place after migration from Drupal to Prismic - can they be deleted at any point?

If we wanted the canonical URL to be human-readable from the start, we would need to build a service to do so, and the service would need to enforce uniqueness (among other things).

We do have human-readable root URLs for website sections.

User requirements:

**Options:**

1.  Use link shortening service. [Bit.ly](http://bit.ly) is one that allows custom branding ($348/year)\


    **Pros**: Inexpensive, controlled by Editorial/Marketing, comes with analytics so you can understand how people actually use it; could be traced as a referrer in GA \
    **Cons**: Can’t rely on it for long-term redirects to key landing pages \
    **Best option for**: frequent use for marketing and promotion; tracking direct hits on vanity URL; tracking content experiments
2.  Developers add to redirect list\


    **Pros**: Easy to do; we have complete visibility of all redirects in one place **Cons**: Can’t track redirects in GA - will only report on the canonical URL, not the URL linked/typed in browser (need to work out best way of inferring directness in GA); list will become unmanageable if we don’t establish rules to manage redirect creation \
    **Best option for**: infrequent use for exhibitions, special events; identifying key landing pages across whole site (e.g. /access or /jointhelibrary)
3.  Developers to build new service

    **Pros**: \
    **Cons**: Expensive, distracts from priority work \
    **Best option for**:

All content within our domain has 1 canonical domain (best practice), which _might_ have redirects to that. We should never have a piece of content with 2 URLs, it is a really bad anti pattern and can lead to URL proliferation, SEO issues, and maintainability / scalability issues.

An example of these issues can be found as to how content was referred to on the old Drupal site.

If we are to have URLs that become canonical, but have been decided by another source that is not the identifier of that object:

* We will need to keep track of every domain minted to ensure uniqueness.
* If we would like to change the new, now canonical domain, we will have to ensure automatic redirection of all previous values assigned to it
* If this is to be managed by content managers, a system with sign on / account access will need to be built. We have not built one of these before.

## Marketing redirects

We can set up a vanity/marketing redirect in these cases:

* It’s a key landing page
* It’s meant to be read aloud
* User needs to remember to write it down
* Print to digital transmission

It would be really good to get the user requirements as to what we are solving. e.g. people can easily type something from a pamphlet. That way we could set up a really simple test, put the URL on a pamphlet and track it to see if anyone actually uses it before building a system based on how we think people will use it.
