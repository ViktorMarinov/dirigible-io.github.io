---
layout: samples
title: Messaging
icon: fa-caret-right
group: simple
---

Messaging
===

Develop
--

1. Create a new project and name it **messaging_basic**.
2. Select the *ScriptingServices* sub-folder of the project and open the pop-up menu.
3. Choose *New* -> *Scripting Service*.
4. Choose **Server-Side JavaScript Service** from the list of available templates.
5. Give it a meaningful name (e.g **messaging_basic.js**).
6. Replace the generated code in **messaging_basic.js** with the following:

```javascript

	/* globals $ */
	/* eslint-env node, dirigible */

	var response = require('net/http/response');
	var messaging = require('service/messaging');

	messaging.registerClient("client1");
	messaging.registerClient("client2");

	messaging.registerTopic("topic1");
	messaging.registerTopic("topic2");

	messaging.subscribe("client1", "topic1");

	messaging.send("client1", "topic1", "Subject on Topic 1 from Client 1", "Message from Client1");
	messaging.send("client1", "topic2", "Subject on Topic 2 from Client 1", "Message from Client1");

	messaging.route();
	var messages = messaging.receive("client1");

	for(var i = 0; i < messages.length; i ++) {
		var message = messages[i];
		response.println(message.subject + " -> " + message.body);
	}
	response.flush();
	response.close();

```

<div class="btn-toolbar pull-right">
	<a class="btn btn-warning" href="http://dirigible.eclipse.org/services/ui/anonymous.html?git=https://github.com/dirigiblelabs/sample_service_messaging_basic.git">Run</a>
	<a class="btn btn-info" href="http://www.dirigible.io/api/messaging.html">API</a>
</div>

Discover
--
To discover all available services, you can go to the [Registry](../help/registry.html).

1. From the main menu, choose **Window** -> **Show Perspective** -> **Registry**.
2. The **Registry** perspective represents a view to the enabled runtime content. From its menu, choose **Discover** -> **JavaScript** to open the currently available server-side JavaScript service endpoints.
3. You can see the list of available endpoints, where you can find yours by naming convention: **{project}/{service path}**
