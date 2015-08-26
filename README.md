# FIDASH: FIWARE's Cloud Dashboard

FIDASH is an administration and management dashboard for FIWARE Lab. FIDASH is the dashboard component of the FIWARE FI-OPS tools, a tool suite created to set-up and operate FIWARE Lab nodes and manage the set of federated [OpenStack](https://www.openstack.org/)-based nodes that make up the FIWARE Lab infrastructure.

This project is part of [FIWARE](https://www.fiware.org/).

FIDASH, as FI-OPS dashboard, is the graphical front-end that offers FIWARE Lab admins with a comprehensive access to different backend services, namely:

* OpenStack services for managing offered resources in FIWARE Cloud (running instances, available images, volumes, image flavors, etc);
* monitoring of the underlying infrastructure (CPU, RAM, Disk usage at different levels of aggregation); and 
* verification of the compliance with stablished Service Level Agreements.

FIDASH is a tailored version of [WireCloud](http://conwet.fi.upm.es/wirecloud/) and has such is a hightly-customizable [mashup](https://en.wikipedia.org/wiki/Mashup_%28web_application_hybrid%29) environment that allows the user to easily define functionality and behaviour of the dashboard. The dashboard is made up of multiple widgets that the user can choose, discard, set layout and modify their behaviour. These widget are connected together to perform higher level functions and to provide correct feedback based on actions done by other components; such integration is done through a mechanism called _wiring_.

In addition, FIDASH comes with predefined dashboard set-ups (mashups with instantiated widgets and setted up wiring) for an out-of-the-box usage; nonetheless the user can modify existing dashboard set-ups or create new ones from scratch, in a guided and intuitive manner. Both functionality and appearance can be customized by the user.

The default widgets in FIDASH are:

* Image Details: <https://github.com/fidash/widget-imagedetails.git>
* Instance Details: <https://github.com/fidash/widget-instancedetails.git>
* Volume Details: <https://github.com/fidash/widget-volumedetails.git>
* List Flavors: <https://github.com/fidash/widget-listflavors.git>
* List Images: <https://github.com/fidash/widget-listimages.git>
* List Instances: <https://github.com/fidash/widget-listinstances.git>
* List Volumes: <https://github.com/fidash/widget-listvolumes.git>
* Resources Usage: <https://github.com/fidash/widget-resourcesusage.git>

