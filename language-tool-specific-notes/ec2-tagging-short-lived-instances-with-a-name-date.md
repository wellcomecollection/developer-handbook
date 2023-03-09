# EC2: tagging short-lived instances with a name/date

Sometimes we create short-lived EC2 instances for manual tasks, e.g. if you need a very powerful instance or you want to run code closer to AWS.

If you do, we have an informal convention that you give the instance a **Name** tag that includes:

* your name
* the current date

Examples: "Alex 9 March 2023", "Jamie 2023-03-09", "Mar 9 Alice"

This means we know who owns the instance, and we can tell if it's stuck around longer than originally intended.
