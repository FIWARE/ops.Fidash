Users should be able to log in FIDASH platform at [https://dash.lab.fiware.org](https://dash.lab.fiware.org) using their own FIWARE Lab user. In case a user does not have a FIWARE Lab user, it should be requested at the [IdM GE](https://account.lab.fiware.org/).

The firts time the user tries to log into FIDASH she will be requested to allow access to the application FIDASH.

> Sometimes, this authorization requests does not appear, and the access to FIDASH platform must be retried. And sometimes IdM does not return to FIDASH after authorization, so it has to be done by user browsing again to [https://dash.lab.fiware.org](https://dash.lab.fiware.org).

The main view of FIDASH is an empty dashboard where the user can create her own dashboard from scratch. However, the fastest way to start is instantiating a previously created dashboard, as explained below. The user is able to create multiple dashboards, to modify them (even the ones created instantiating a existing one), or to create themo from scratch.

In any case, the button for all of the dashboard-related tasks, including accessing existing ones, deleting, creating new ones or accessing their settings is this one: ![menu button](images/menu.png)

### Instantiate dashboards

In case a previously created dashboard is to be used, either by having been created by the user, uploaded by her or it is a publicly available dashboard, as they are on the platform.

In FIDASH, dashboards appear as mashups in the **My Resources** section. 

![Access to My Resources](images/my-resources.png)

Clicking on _My Resources_ button takes the user to the full list of resources, where some of them are labeled with the tag **mashup**. Those are the dashboards that can be instantiated. 

![My Resources screen](images/my-resources-screen.png)

Documentation of widgets, operators and mashups is accessible on that screen by clicking on any of them.

In case the user wants to deploy one of the dashboards (the mashups), she must back to the dashboard view, use the menu button (![menu button](images/menu-small.png)) and chooose **New workspace** option. In next window, a lookup icon displays the list of mashups (the dashboards), and the user does only have to choose one of them by clicking on the select button.

![Choose dashboard](images/choose-mashup.png)

If no name is specified, the new dashboard will inherit the name of the mashup. In any case, it will appear on the list of workspaces accessible through the ![menu button](images/menu-small.png) button.

This dashboard can be customized as the user wishes:

* Size of the widgets can be changed dragging the lower-right corner of them
* Position of the widgets can be changed by clicking on the top bar of them
* Widgets may have some options accessible through their settings menu that appears when the mouse stops over the top-right corner of the widget ![Choose dashboard](images/widget-menu.png)

User can also remove widgets (cross next to the options menu of the widget), add new widgets or modify the behaviour through wiring. Next sections describe the latter options in detail.

### Instantiate widgets

In the desired work-space, click the plus button for adding widgets is to be used.

![add widget button](images/add-widget.png)

The available widgets will appear in a left-sliding window. Another add button is available at each widget header so as to add it to the current workspace.

![add to workspace](images/add-to-workspace.png)

Widgets appear with a default size and in the best available empty space inside the workspace. Please be aware of the tab functionality at the bottom of the page, in case big dashboards are desired. Widget size and position can be changed and adjusted using its window controls (bottom-left and right corner to resize and title bar to drag).

### Defining behaviour through wiring

FIDASH widgets communicate among themselves so as to create a composite application made up from the collaboration of the different widgets instantiated in a dashboard. Widgets generate events containing data of items of interaction (mainly identifiers of VMs, volumes, etc), and what other widgets receive such events and act accordingly (e.g. showing the details of the received VM id) is decided by the dashboard user defining the wiring among the widgets. This is done on the **wiring tool**, that is accessible through its icon:

![wiring button](images/wiring-button.png)

On the wiring tool, all the widgets deployed on the dashboard appear at the leftmost side of the screen. These elements are to be dropped on the middle panel so as to define the wiring (namely connect output endpoints with input endpoints).

As they are at the center panel, input and output endpoints of the widgets are shown. Input endpoints are shown as orange circles at the left of the widgets, whereas output endpoints are green circles at the right side of them.

![wiring endpoints](images/wiring-before.png)

If the user wants that an event generated at a given widget (for example, after she clicking on an VM image ID in a table) is reproduced on some other widget (e.g. showing the details of that image) she has to drag the corresponding output endpoint to the corresponding input endpoint. In case multiple input and output endpoints, or when their related actions are not easily understood by the simple description, the documentation of the widget describes precisely those actions and effects.

It is noteworthy indicating that the selection of a certain endpoint highlights the compatible endpoints that can be connected with the one selected. In FIDASH this implies that choosing an endpoint outputting an image ID highlights the input endpoints where an image ID is expected. Due to the open nature of the WireCloud wiring technology, it is not a constraint, and a user can decide to connect different types of events at his own risk (since they do only send text data), but the result might not be satisfactory.

![wiring endpoints](images/wiring-assistance.png)

Finally, the created wire appears as a pipe linking both endpoints, what implies that whenever the widget source of the event produces it, the event with the associated data is immediately taken by the platform to the consumer of that event.

The input and output endpoints can have as many wires connected as desired, allowing the user to completely define the behaviour of her dashboard.

### Basic widget connections

Created widgets for FIDASH are designed maximizing the input and output endpoints that those widgets can handle. This is done so as to provide the maximum flexibility to FIDASH users. However, there are typical connections that are the basis for most dashboards.

All the widgets related to OpenStack services are divided into two categories, listing widgets and detail widgets. Listing widgets show list of images, volumes, etc, plus some basic information, and rely on detail widgets for showing further information. These pairs of widgets are to be connected together (in case a user wants to deploy both on her dashboard). But nonetheless some of them offer some further functionality (e.g. ListInstance or DetailInstance widgets can generate image ID events, that the user can wire to the same or other instance of DetailImage in case she wants to make use of that option).

An example of connections of a simple dashboard containing one instance of every widget would be the one shown in the image below. In this case, Detail image would display the details of an image clicked on the details of an instance, on the list of instances (has a image column) or on the list of images.

![basic wiring](images/basic-wiring.png)

### Publishing your own dashboard

Once a dashboard is created, having settled the desired layout, the wiring, the properties, etc., it can be saved for the future, of for sharing with other users. This can be done by clicking on the menu button (![menu button](images/menu-small.png)) and choosing _Upload to my resources_. User must indicate vendor, version number, email, and some brief description. On other tabs an icon can be added (170x80 px), and some other options such as block the widgets in the mashup, block the connections, or embed the widgets or operators inside the dashboard (not only linking them by reference).

![Upload dashboard](images/upload-dashboard.png)

After uploading the dashboard, **My Resources** section will display a new resource with the chosen name. This dashboard can be instantiated or downloaded (to be shared with others).