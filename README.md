# FIDASH: FIWARE's Cloud Dashboard

FIDASH is an administration and management dashboard for FIWARE Lab. FIDASH is the dashboard component of the FIWARE FI-OPS tools, a tool suite created to set-up and operate FIWARE Lab nodes and manage the set of federated [OpenStack](https://www.openstack.org/)-based nodes that make up the FIWARE Lab infrastructure.

This project is part of [FIWARE](https://www.fiware.org/)[1].

## Description

FIDASH is a tailored version of [WireCloud](http://conwet.fi.upm.es/wirecloud/)[2] and has such is a hightly-customizable [mashup](https://en.wikipedia.org/wiki/Mashup_%28web_application_hybrid%29)[3] environment that allows the user to easily define functionality and behaviour of the dashboard. The dashboard is made up of multiple widgets that the user can choose, discard, set layout and modify their behaviour.

These widgets offer specific functionality such as display a list of instances or synchronize the flavors of some FIWARE Lab. Widgets rely on REST-based APIs offered by the different OpenStack services, the SLA Manager, XIFI Monitoring or other services created in FITOOLKIT project to give support for certain actions. Some services are directly accessed, though others use some libraries to hide the complexity of the APIs, such as the [jstack]( https://github.com/ging/jstack)[4] library for accessing OpenStack services in FIWARE Lab deployments. Authentication is managed by the underlying WireCloud platform against the Identity Management (IdM) and the keystone Proxy present on all FIWARE Lab nodes, and authorization relies on the user rights present at the IdM.

These widget are connected together to perform higher level functions and to provide correct feedback based on actions done by other components; such integration is done through a mechanism called _wiring_, that send asynchronous messages with data among themselves (events). User of FIDASH is in control of that wiring, and can connec/disconnec widgets at will, modifying the behaviour of the dashboard.

In addition, FIDASH comes with predefined dashboard set-ups (mashups with instantiated widgets and setted up wiring) for an out-of-the-box usage; nonetheless the user can modify existing dashboard set-ups or create new ones from scratch, in a guided and intuitive manner. Both functionality and appearance can be customized by the user.

## Features implemented

FIDASH, as FI-OPS dashboard, is the graphical front-end that offers FIWARE Lab admins with a comprehensive access to different backend services, namely:

* OpenStack services for managing offered resources in FIWARE Cloud. The elements managed at FIDASH are:
	* running instances or VMs, they can be listed, detailed, searched, filtered, deleted and rebooted. Simple creation functionality is also provided
	* images, that can be listed, detailed, searched, filtered, made public or protected, and created from file or remore URL. Simple launch functionality is also provided
	* volumes, that can be listed, detailed, searched, filtered, and attached to volumes
	* flavors, that can be listed, detailed, searched and filtered. Edition and creation of new ones is also implemented but requires administrative priviles.
* monitoring of the underlying infrastructure, including CPU, RAM, Disk usage and floating IPs, indicating the free and reserved resources in a graphical format per region.
* verification of the compliance with stablished Service Level Agreements.

The default widgets in FIDASH are:

* Image Details: <https://github.com/fidash/widget-imagedetails.git>
* Instance Details: <https://github.com/fidash/widget-instancedetails.git>
* Volume Details: <https://github.com/fidash/widget-volumedetails.git>
* List Flavors: <https://github.com/fidash/widget-listflavors.git>
* List Images: <https://github.com/fidash/widget-listimages.git>
* List Instances: <https://github.com/fidash/widget-listinstances.git>
* List Volumes: <https://github.com/fidash/widget-listvolumes.git>
* Resources Usage: <https://github.com/fidash/widget-resourcesusage.git>
* Embedded SLA Manager: <https://github.com/fidash/widget-embedded-SLAManager>
* SLA Manager: <https://github.com/fidash/widget-embedded-SLAManager>


## Installation manual and verification

To see how to deploy FIDASH and how to test that the installation is correct, please refer to the [Deploy Guide](docs/deploy/deploy.md).

## User manual

The instructions for FIDASH users, including the creating dashboards, customize existing ones and modify their behaviour is described in the [User Guide](docs/user_guide/user_guide.md)

## Know issues

Widget can work without major problems with HTTP connection, but please be aware that this can create a security problem. For HTTPS connection could be needed that the server sends some HTTP Headers to enable the 
visualization of the data or to relax some policies (e.g. [Same-origin policy](https://en.wikipedia.org/wiki/Same-origin_policy) ).

In modern browsers, linking to an HTTP resource from an HTTPS page is forbidden and a slight notice might be shown by the browser (Firefox and chrome show a shield icon next to the address bar) to allow these kind of connections. During the development of FIDASH and the associated back-end services, some HTTP services might be used, and user should allow these types of connections manually (by clicking on that shield in the case of Firefox and chrome).

FIDASH widgets are developed and tested on Chrome and Chromium browsers. Firefox does not render correctly the Resources Usage widget. However WireCloud platform, on which FIDASH is based, is tested on Firefox and chrome browsers though other browsers supporting HTML5 standards will probably be 100% compatible, but it is not guaranteed.

## Licence

Apache License, Version 2.0, January 2004

## References

1. FIWARE: [https://www.fiware.org/](https://www.fiware.org/)
2. WireCloud[http://conwet.fi.upm.es/wirecloud/](http://conwet.fi.upm.es/wirecloud/)
3. Mashup definition at Wikipedia [https://en.wikipedia.org/wiki/Mashup_%28web_application_hybrid%29](https://en.wikipedia.org/wiki/Mashup_%28web_application_hybrid%29)
4. jStack library: [https://github.com/ging/jstack](https://github.com/ging/jstack)
