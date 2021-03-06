---
old_url: key_concepts.htm
title: "Data Sources"
active_menu_item: developers
class_name: developers
full_width: true
---


Any report or dashboard will need to access data. This data can be data in a database, LDAP directory, spreadsheet or other data source. In fact, AC can produce a single report that combines data from more than one different data source type.

So the first thing you will need to set up are [Connections](/developers/documentation/product-guide/the-console/console-tabs/connections/) and [Queries](/developers/documentation/product-guide/the-console/console-tabs/queries/) . These are set up in the AC Console and enable you to configure re-usable data sources.

You can also control Views and Drill-Downs using [Views scripting functions](/developers/documentation/scripting-apis/client-api/data-view-functions/) .

Please note, these are client side functions and so inherently insecure, however, we have introduced Server Side Javascript support and these functions are available on a server side API that is be secure. See [Server Side Scripting Overview](/developers/documentation/scripting-apis/server-side-scripting-overview/) .
