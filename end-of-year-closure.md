# End-of-year closure

Wellcome’s London offices close between Christmas and the New Year, which means about a fortnight when no developers are working.

However, Wellcome Collection remains open to the public, and it's important that the site remains up and working over this period. Ideally, there should be nothing that requires developer attention until the offices re-open in January.

Although we can never guarantee there won’t be an incident, we can try to minimise the risk in the weeks before the end-of-year closure.

## Maybe don’t deploy that big change?

We don't have a formal “change freeze” period, but try to avoid deploying big changes close to Christmas – less people in the office means we might be slower to spot bugs in prod, and you’ll have less help if something goes wrong.

This does mean we might have a rocky period in January, when we deploy everything we “bottled up” at the end of the year – but that’s better than deploying it before Christmas and causing an out-of-hours incident.

(In practice this tends to happen pretty naturally, as people gradually disappear for their Christmas breaks, and output slows down accordingly.)

## Test any date-sensitive services beforehand

This includes:

* the display of opening times on the website\
  The Editorial team is responsible for updating and publishing "modified opening times" in Prismic for the Café, Shop, Library and Galleries & Reading room.  Once this is done, the website should display the exceptional closure days.
* the date picker for requesting items (we can [disable this if necessary](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/docs/turn-off-requesting.md), but we'd rather not)
  * Date options for on-site items depend on the Library opening times (see above)
  * Date options for off-site (Deepstore) items depend on a separate (Deepstore) Collection Venue type in Prismic. The Digital team's Delivery Manager is responsible for updating and publishing Deepstore "modified opening times". Sarah Bird (Collection Storage Manager) can confirm Deepstore exceptional closures. &#x20;
* NOTE on the above: Deepstore orders are managed manually by the LE\&E team and made on average once a week at their discretion. As of December 2024 we set the Deepstore venue in Prismic to be closed the week before the library closes, and until the library reopens in January.&#x20;

Checking that the date picker is going to behave correctly during the closure:

* Once the Modified opening times have been updated in Prismic, use `api/scripts/holiday_closure_test.ts` in the content-api repo to check what dates will be displayed in the date picker dropdown.&#x20;

## **Turn off services that won’t be used**

This is a good rule in general, but especially when we won't be working for an extended period – don't leave unused or temporary services running.

e.g. we often run multiple instances of the catalogue pipeline, but we should only keep the live pipeline running over the closure.
