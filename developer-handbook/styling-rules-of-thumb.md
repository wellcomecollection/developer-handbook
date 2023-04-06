---
description: >-
  Always a work in progress, these rules of thumb should be considered open to
  discussion, always to be brought back up and decided upon.
---

# Styling: rules of thumb

As the team grows and more people are heavily involved with styling, we thought it’d be good to have a chat to align on our best practices with the aim of documenting them for the rest of the team, as well as new joiners. We don't see this documentation as strict rules to be followed, but as rules of thumb, which could also help knowing what to flag in code reviews.

### Styled-components

[Styled components](https://styled-components.com/) (SC) is a very useful tool for styling repetitive elements only once, and can help with the readability of a component in making them less bulky. If the wider component file is very complex, having readable, use-focused names for various elements is quite useful. For example, [the `Footer` component ](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/common/views/components/Footer/index.tsx#L163)could be considered hard to read and was split in smaller chunks with readable names for all sections. Some things we abide by;

1. If an element is repeated at least once, or has complex styles, create an SC for it.&#x20;
2. If an element only has attributes and no styling, it's not worth making into an SC. SC should be used for styling first and otherwise be kept simple.
3. Styling a component inline is ok for 1-2 properties. If it grows bigger, do consider creating an SC instead.&#x20;

**To be discussed:**

1. If a styled-component is created, which attributes do we move over, aside from the ones that affect the styles (e.g. `className`)? All of them? A select few?
   1. Still TBD; should we treat them as defaults, then override them if necessary?

### Separate styles files

[As seen in `identity`](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/identity/webapp/src/frontend/components), or even in some components in the other repos, files like `ComponentName.styles.ts` can be useful when there are a lot of SCs being declared within the same file. It makes it easier to focus on the components' functionalities and understand at a glance what it is doing.  It can also be useful for when a complex component has multiple subfiles (e.g. [`Footer.Nav,ts`](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/common/views/components/Footer)), and they need to share styles.  Again, it's a judgement call when that is necessary.

### Utility classes

We've now decided to move away from them, but we've discussed finding them useful for certain things, such as visibility rules. Most of them will slowly be removed ([see PR with most decisions documented](https://github.com/wellcomecollection/wellcomecollection.org/pull/9551)), and it can always be a conversation as to whether we'd like to delete more of them or create new ones.&#x20;

The cleaning up was done for `utility-classes.ts`, but we are aware that more of them exist (see `typography.ts`, for example). These might be part of a wider review, but do always question them if need be. Ideally, going forward, we are moving away from utility classes.

### Utility components

[Can be found in `common/views/components/styled`](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/common/views/components/styled), it is another way of reusing the same styles, a project-wide, shared, SC. There aren't that many of them, and they only exist within common. Do we want to use that more? Move them to become full-on Components? It feels like yet another method that maybe we could simplify, but this topic is still to be discussed.
