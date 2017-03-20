Using Alerts
============

The Open Recipe Format allows each step of a recipe to include extra, computer-readable information about that step. For instance, a duration may be stored, such as 25M (25 minutes). Durations are based on the Unix date command, and include:

-   S: Seconds
-   M: Minutes
-   H: Hours
-   d: Days
-   W: Weeks
-   m: Months
-   Y: Years

Please note that as with the date command, these abbreviations are case-sensitive; M refers to minutes, while m refers to months.

Long-Term Durations
===================

The first question in many cooks' minds will be, why worry about anything longer than hours? Bear in mind that this format is intended to be usable in any situation where food is to be prepared. The following are all valid use cases:

-   Curing a duck breast prosciutto for several days.
-   Dry-curing an Italian sausage for several weeks.
-   Allowing vanilla beans to soak in vodka for several months.
-   Allowing whiskey to age in barrels for several years.

Software-Based Alerts
=====================

With these considerations in mind, software can be written that helps the cook manage recipes, and alert the cook when an action needs to be taken.

For instance, mobile recipe software can not only display the steps of a recipe, but also allow a cook to press a button when putting a tray of cookies into the oven, which will trigger an alarm 12 minutes later to remove them from the oven. Software designed for cheesemakers can be set up to add an item to a person's calendar, or send an email, when a particular batch of cheese needs to be checked. Such software should assume that multiple batches are being processed at once, and allow the food producer to store their own internal storage information (bin codes, batch dates, etc) within the software.

Examples
========
