---
layout: docwithnav-paas
assignees:
- vsosliuk
title: Basic MQTT authentication
description: ThingsBoard MQTT based authentication.
options:
    0:
        image: /images/user-guide/basic-mqtt/client-id.png  
        title: 'MQTT Clients will be able to connect with any username or password if they specify correct Client ID.'    
    1:
        image: /images/user-guide/basic-mqtt/username-password.png  
        title: 'MQTT Clients will be able to connect with any client ID if they specify correct Username and Password.'
    2:
        image: /images/user-guide/basic-mqtt/no-password-check.png  
        title: 'Password is optional'
    3:
        image: /images/user-guide/basic-mqtt/client-id-username-password.png  
        title: 'MQTT Clients will be able to connect if they specify correct combination of Client ID, Username and Password'    
---

{% assign docsPrefix = "paas/" %}
{% include docs/user-guide/basic-mqtt.md %}