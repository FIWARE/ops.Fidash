# FIDASH User Guide

### Users and permissions

Users should be able to log in FIDASH platform at [https://dash.lab.fiware.org](https://dash.lab.fiware.org) using their own FIWARE Lab user. In case a user does not have a FIWARE Lab user, it should be requested at the [IdM GE](https://account.lab.fiware.org/). User roles and permissions are inherited from the ones they do have on the cloud portal or assigned on FIDASH application for administration purposes. Issues with user rights should be addressed to [fiware-tech-help@lists.fiware.org](mailto:fiware-tech-help@lists.fiware.org) clearly indicating *FIDASH* as the destination of the request.

# Dashboard creation and editing

## Using a pre-created dashboard

FIDASH comes with pre-created dashboards that can be instantiated and used in seconds. To do this, button ![menu button](images/menu.png) shall be used to create a new dashboard. In the template-selection screen, click the search button, and all the available dashboards will appear.

![template selection](images/template-selection.png)

Select button of the desired dashboard is to be clicked. If no name is specified, new workspace will be created with the name of the dashboard.

![dashboard selection](images/dashboard-selection.png)


## Dashboard customization

An existing mashup or a new one (accessible from the mashup menu button ![menu button](images/menu.png)) shall be used.

The first time the user tries to log into FIDASH she will be requested to allow access to the application FIDASH.

> Sometimes, this authorization requests does not appear, and the access to FIDASH platform must be retried. And sometimes IdM does not return to FIDASH after authorization, so it has to be done by user browsing again to [https://dash.lab.fiware.org](https://dash.lab.fiware.org).

The main view of FIDASH is an empty dashboard where the user can create her own dashboard from scratch. However, the fastest way to start is instantiating a previously created dashboard, as explained below. The user is able to create multiple dashboards, to modify them (even the ones created instantiating a existing one), or to create them from scratch.

In any case, the button for all of the dashboard-related tasks, including accessing existing ones, deleting, creating new ones or accessing their settings is this one: ![menu button](images/menu.png)

### Instantiate dashboards

In case a previously created dashboard is to be used, either by having been created by the user, uploaded by her or it is a publicly available dashboard, as they are on the platform.

In FIDASH, dashboards appear as mashups in the **My Resources** section. 

![Access to My Resources](images/my-resources.png)

Clicking on _My Resources_ button takes the user to the full list of resources, where some of them are labeled with the tag **mashup**. Those are the dashboards that can be instantiated. 

![My Resources screen](images/my-resources-screen.png)

Documentation of widgets, operators and mashups is accessible on that screen by clicking on any of them.

In case the user wants to deploy one of the dashboards (the mashups), she must back to the dashboard view, use the menu button (![menu button](images/menu-small.png)) and choose **New workspace** option. In next window, a look-up icon displays the list of mashups (the dashboards), and the user does only have to choose one of them by clicking on the select button.

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

# Usage of components

## Regions selector

This widget has no useful functionality on its own, but can be combined with some other widgets so as to simplify the selection of regions. Many of the widgets of FIDASH do offer the possibility to choose among the set of regions to operate. This is the case of monitoring widgets and OpenStack-based ones. In that case, widgets individually allow the selection of regions, and they do internally save that user preference. However, when a user wants to a set of widgets in a dashboard operate over the same set of regions, it is not agile configuring all of them. This is where Regions Selector widget simplifies the task.

This widget exposes the full list of regions and sends, using the wiring mechanism, the list of selected regions to any widget connected to it. Therefore, it is up to the user to decide what widgets to wire to it.

![Select Region widget](images/select-region.png)

The wiring connections must be defined on the wiring tool as described above, linking the _output endpoint_ of Select Region with the _input endpoint_ of the desired widget/s. This is an example of the widget instantiated and wired to three more instantiated widgets:

![SelectRegion widget wiring example](images/select-regions-wiring-example.png)

## Data usage (top tenants)

Data usage is a useful widget to see, at a glance, what are the most resource consuming tenants, and what resources might be over- or under-provisioned. It does make use of the data usage feature inside monitoring infrastructure, which collects and reports an anonymized list of top tenants on different measures: number of instances, total RAM reserved, number of vCPUs, percentage of RAM used and percentage of CPU used. While some of them are absolute values representing amount of resources reserved, others indicate the degree of usage of those resources. Therefore, they can be easily compared.

![Data usage widget](images/data-usage.png)

Top tenants can be also be sorted and listed according to any of that 5 measures by using the top 5 coloured buttons, that obtain the data sorted by that specific column.

Data inside columns is scaled according to the highest value in the set. As an example, in RAM column where values migh be 2 GB, 8 GB and 12 GB, the latter would be represented with a coloured bar of 100% of width, scaling the rest accordingly. It does also happens on percentage values, which are not adjusted up to 100%, but up to the highest value in the set of tenants to be shown.

Specific values can also be read by leaving the cursos over a row for some seconds:

![Data usage tooltip](images/data-usage-tooltip.png)

## Flavor Sync

Glance Sync functionality is composed of two widgets:

* **Compare Flavors**: It lists reference flavors on the left, and flavors of the current region on the right. The current region is chosen among the ones that the user is _infrastructure owner_. User can select one flavor on each column, and according to that selection, the widget allows the user to:
	* copy ![copy](images/copy.png) (left-column selected to current region)
	* replace ![replace](images/replace.png) (right-column selected with left-column selected)
	* delete ![delete](images/delete.png) (right-column selected)

	Besides, widget eases the task of comparing by hiding ![hide/show equals](images/hide-show equals.png) the flavors that are compatible on the left and on the right. And the selections can be cleared ![clear](images/clear.png).
	
	![compare flavors](images/compare flavors.png)

* **Show flavor differences**: with the widgets selected on **compare flavors** widget, this one shows their details highlighting the differences.
 
    ![show flavor differences](images/show flavor differences.png)

## Maintenance calendar

Calendar widget is a horizontal-based time-line, where each region is placed on a different row, plus one for no-maintenance requests.

This widget depends on specific **roles** assigned to the user. According to the roles, display and actions differ:

* For **non-authorized users**, the calendar is read-only, displaying the maintennance events of every region. Every row is shown on grey color
* For **infrastructure owners on certain regions** the calendar allows the creation events. The user must have been granted the role `InfrastructureOwner` on those regions, which will appear in white color denoting they are writtable.
* For **uptime requesters**, who are users allowed to request _no-maintenance_ periods, thus requireing the role `UptimeRequester`, the first row does appear on white and is writtable.

![calendar](images/calendar.png)

> Widget might take some seconds to fully load regions, roles and events. On this time it does not display rows.

### Creation, deletion and edition of events

Rows in grey color are not writable by the user, whereas he does have permission to write on white ones according to her designated roles. A regular lab user shall see all the calendar marked in grey.

By _double clicking_ on a certain white row (whenever user is authorized), a modal dialog appears to enter details. Textual description must be written here, but timing can be established back on the calendar. By _clicking_ on an event that the user can modify, interface changes being able to delete it or, more important, drag edges to the desired values for modifying start and end date and time.

![calendar edit](images/calendar edit.png)

### Modifying the displayed time-frame

Besides the dashboard option to resize the calendar, that might display every region or not, and does increase/decreas the time-frame displayed (on horizontal resizes), the displayed time-frame can be modified in two senses:

* Moving to future or past dates by horizontal _dragging_ on any part of the calendar
* Zooming by clicking _shift_ key while using the scroll. It does produce horizontal zooming, allowing to select the time-frame to be shown. Zooming function ranges from years to hours level.

### Exporting to ICS

FITOOKIT did create the back-end, and a public ICS calendar is exported with the events of every region in a single calendar. This calendar, linked to the ![ical link](images/ical.gif) image in widget, is accessible at URL [http://130.206.113.159:8085/api/v1/ics/maintenanceCalendarFiwareLab](http://130.206.113.159:8085/api/v1/ics/maintenanceCalendarFiwareLab), and can be integrated in Outlook, Thunderbird, OS X's Calendar, Google Calendar, etc. This would be the basic instructions for integrating the calendar:

* Microsoft Outlook: On Calendar Section, `Open calendar` -> `From Internet`, and paste the URL
* OS X's Calendar: Click on `File` -> `New calendar subscription...` and paste the URL
* Google Calendar: Go to calendar settings, and click on the link `Browse interesting calendars` which is located below the list of personal calendars. On next screen click on `Add by URL` and paste the URL.

    > Google Calendar does refresh external ICSs on an un-specified frequency that seems to be around 24 hours.


## Monitoring

### Monitoring regions

General data about different regions is shown in **Monitoring Regions** widget. It shows virtual CPUs, RAM, disk space and public IPs in a percentage ratio of total/used and a circular graph. It does also indicate real values on tooltip when mouse is over a graph. For CPU and RAM usage, virtual values (applied the overcommit ratio) are shown.

Widget is flexible in two ways:

* it allows choosing one or many regions, via its region selector or receiving them by wiring from the **region selector widget**. Each region is shown in a specific card, and those cards are arranged in columns automatically according to the vertical and horizontal space of widget vs cards.
* it allows user to focus on the desired measures (vCPU, RAM, disk and IP addresses). It works together with the selection of regions, and allows for a flexible creation of specific purpose views.

It's worth saying that the widget, as all of them, can be instantiated multiple times, focusing a given instance on a specific purpose, such as global status of computing or free IP addresses, or monitoring of the set of regions of interest (e.g. the ones hat are hosting one application).

## OpenStack management widgets

The set of OpenStack-based widgets allow for a basic management of personal elements on FIWARE Lab. It does not intend to replace FIWARE Cloud interface, but to serve a subset of its functionality inside FIDASH, so as users can create dashboards adding information about her own resources. As a differentiation, OpenStack-based widgets are by default _multi-region_, so images, instances, volumes and flavors can be browsed of one, all or several regions at once.

### Instances

User instances can be obtained from any region using [ListInstances](https://github.com/fidash/widget-listinstances) widget, and the details of a given instance can be seen using [DetailsInstance](https://github.com/fidash/widget-detailinstance) widget. When a user clicks on an instance of the list, it is shown on the details widget. Both widgets used together can be seen in following image:

![ListInstances and DisplayInstance widgets](images/instances-widgets.png)

Instances can be rebooted, but further options are to be done on Cloud portal.

The regions where to search for instances can be chosen using the button ![select regions button](images/select-region-button.png), where the list of regions appears and user can select them:

![select regions](images/list-instances-select-region.png)

Alternative, _Regions Selector_ widget can be instantiated and wired to the list of instances so as to update the list as soon as it is modified in _Regions Selector_ widget.

#### Wiring

_Detail Instance_ widget does require receiving instance ID through wiring. Therefore, the easiest way is to link it to _List Instances_ widget.

Moreover, these OpenStack management widgets do perform authentication externally, using an operator called _OpenStack auth operator_. Therefore, such operator must be also instantiated and linked to these widgets. Besides, _Regions Selector_ widget might be also used to externalize the selection of regions and to be shared among different widgets, such as _List Volumes_ and _List Flavors_, to be described below.

This is an example of the required wiring for working with instances:

![Wiring of widgets about instances](images/instances-wiring.png)

### Volumes

User volumes are listed and detailed with _List Volumes_ widget and _Detail Volume_ widget. These widgets work simmilar to the images-related widgets, operating at any region and selecting the regions internally or through the _Regions Selector_.

![Volumes widgets](images/volumes-widgets.png)

Volumes can be created using the ![plus button](images/plus-button.png) button, only allowing basic options such as name, size or region. Please bear in mind that the selected region might not be currently selected, so recently created volume might not be seen until that selection is displayed.

#### Wiring

Volume ID is sent to the _Details Volume_ widget by the _List Volumes_ widget whenever a user clicks on a row of the list.

Both widgets do require external OpenStack authentication details through the _OpenStack auth operator_, so it must be connected to them. It is worth mentioning that a single instance of such operator can be connected to any widget receiving authentication details through wiring.

![Wiring of widgets about volumes](images/volumes-wiring.png)

### Images

The widgets working with images are similar to the aforementioned ones working with volumes and instances. The main difference is that images show can be private to the user, or public in a given region.

![images widgets](images/images-widgets.png)

Images can also be added from disk or URL by choosing basic parameters, by using the ![plus button](images/plus-button.png) button on the list widget. And they can be set to run with :

![create an image](images/image-create.png)

#### Wiring

Image ID is required to be sent from _Image List_ to _Image Detail_, as a basic connection. Besides, authentication using _OpenStack auth operator_ is also required.

As an extra detail, instance-based widgets, both _Instance List_ and _Instance Detail_ do offer the image ID of the image on which is based the instance, so _Image Detail_ can be also used to display the image related to an instance, not requiring _List Image_ widget.

![Example wiring of images widgets](images/images-wiring.png)

### Flavors

Flavors can be easily listed with _List Flavors_ widget. This widget is not administrative, so it has not flavors-managing functions such as described in Sync Flavors section. Indeed, authentication is more simple, so it does not need _OpenStac Auth Operator_.

![List Flavors widget](images/list-flavors-widget.png)
