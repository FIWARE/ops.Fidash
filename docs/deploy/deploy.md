# FIDASH deployment documentation

## Introduction

The document describes the installation of the FIDASH component, the modification and creation of dashboards, the permissions needed to operate with the different services, and other technical details relevant of the usage of the component.

## Installation of the environment

FIDASH environment at the time of writing is executed inside public WireCloud instance in FIWARE Lab at [https://mashup.lab.fiware.org](https://mashup.lab.fiware.org).

> In the future FIDASH will require a customized version of WireCloud. This document will be updated to describe the required steps to include the installation of such custom WireCloud instance together with the configurations and customizations required.

> Since a public instance, and not a dedicated one, is being used at the time of writing, FIDASH currently requires the user to manually upload widgets to its own set of resources inside [https://mashup.lab.fiware.org](https://mashup.lab.fiware.org) following the instructions described below.

### Uploading widgets

Widgets must be packaged as zip-compressed files using `.wgt` extension to be uploaded in FIDASH, however their package they can be downloaded from repositories or created from the source code. To upload widgets, go to the **My Resources** section inside [wirecloud public instance](https://mashup.lab.fiware.org), click on **Upload** button and then drag all the desired widgets.

![Access to My Resources](images/my-resources.png) ![upload button](images/upload.png)

Widgets can now be found on the **My Resources** section, where user can see the details such as their version and delete or manage existing widgets. However, widgets are not yet instantiated in any dashboard or mashup.

> At the time of writing widgets are available as `.wgt` files in the [developers repository manager](https://repo.conwet.fi.upm.es/artifactory/webapp/browserepo.html), under the `widget-release` folder. According to FIWARE developer guidelines, binaries and source code are being migrated to GitHub and will be available under the [FIDASH organization at GitHub](https://github.com/fidash).

## Dashboard creation

An existing mashup or a new one (accessible from the mashup menu button ![menu button](images/menu.png)) shall be used.


### Instantiate widgets

In the desired workspace, click the plus button for adding widgets is to be used.

![add widget button](images/add-widget.png)

The available widgets will appear in a left-sliding window. Another add button is available at each widget header so as to add it to the current workspace.

![add to workspace](images/add-to-workspace.png)

Widgets appear with a default size and in the best available empty space inside the workspace. Please be aware of the tab functionality at the bottom of the page, in case big dashboards are desired. Widget size and position can be changed and adjusted using its window controls (bottom-left and right corner to resize and title bar to drag).

### Defininig behaviour through wiring

FIDASH instance will be deployed with a default configuration that allows the defaults widgets to operate together, nonetheless the user can upload they widgets and wire them with the others. FIDASH inherits WireCloud's system to highlight matching inputs/outputs that are using the same *friendly code* so it is easier for the user to see which endpoint of the widget can be connected with.

> Typical deployments (normal connections). It must have a sentence indicating the open nature of FIDASH, we're only indicating basic usage, but since widgets are designed to be as widely connectable as possible, the user is free to make his own dashboards (including connections)

## Permissions

Since FIDASH is composed by widgets with multi-region capabilities, you should have access to all the region you need to monitor or to manage; in addition a special access is requires to access SLAManager API.

### How to get Multi-Region access

### How to get SLAManager access

> What is needed in order to work with different componenst

> 	* OpenStack (now only per-tenant things but we should require admin permissions)
> 	* SLAManager
> 	* XIFI monitoring

## Other considerations

Widget can work without major problems with HTTP connection, but please be aware that this can create a security problem. For HTTPS connection could be needed that the server sends some HTTP Headers to enable the 
visualization of the data or to relax some policies (e.g. [Same-origin policy](https://en.wikipedia.org/wiki/Same-origin_policy) )
> Browser support, HTTP vs HTTPS, ...


