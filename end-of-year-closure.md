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

* the display of opening times on the website
* the date picker for requesting items

If you’re running the website locally, you can [make the front-end code think it’s a different date](https://github.com/wellcomecollection/wellcomecollection.org/blob/9f50768da9c8fb7029985e16b16679056c549431/common/utils/dates.ts#L4-L19), so you can see how it will behave during the closure. You can check it's going to behave correctly, and check it matches the expectations of staff who’ll be working during the closure (e.g. see these [screenshots of the item picker](https://github.com/wellcomecollection/wellcomecollection.org/issues/8976) in the Christmas 2022 closure).

## **Turn off services that won’t be used**

This is a good rule in general, but especially when we won't be working for an extended period – don't leave unused or temporary services running.

e.g. we often run multiple instances of the catalogue pipeline, but we should only keep the live pipeline running over the closure.
