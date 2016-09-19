# FIDASH deployment documentation

## Introduction

The document describes the installation of the FIDASH component, the modification and creation of dashboards, the permissions needed to operate with the different services, and other technical details relevant of the usage of the component.

## Installation of the environment

FIDASH is based on WireCloud. Version 0.9.2 is recommended in case provided style wants to be used as is. Public instance of WireCloud ([https://mashup.lab.fiware.org](https://mashup.lab.fiware.org)) might be used for testing some widgets, but roles are not defined, so not all functionality can be used.

### WireCloud installation

A regular WireCloud instance is required. Please follow the instructions on the [WireCloud installation guide](https://github.com/Wirecloud/wirecloud/blob/develop/docs/installation_guide.md) or use a pre-created image.

After the basic installation, integration with the IdM GE musth be done, as described in such guide. Besides, Apache2-based running is also recommended.

### Theme

It is not mandatory to modify the theme. A customized version of the WireCloud FIWARE theme has been created with specific logos and branding, and can be used by copying the [https://github.com/fidash/fiware-fidash/tree/master/theme/fidashtheme](https://github.com/fidash/fiware-fidash/tree/master/theme/fidashtheme) folder on the WireCloud installation directory and modifying the `THEME_ACTIVE` directive on `settings.py` to `fidashtheme`.

### Roles

Different roles are used in Widgets and in backend services. These roles must be defined for certain users in the IdM application created for integrating the WireCloud instance with IdM.

Some roles are general, such as `UptimeRequester` for calendar or `InfrastructureManager` for image synchronization. But the `InfrastructureOwner` is not to be granted to the user in the app, but to be granted to the user in an organization that matches the region name (adding the string " FIDASH"). This role is for accounts allowed to manage elements inside a region, though that users should also have OpenStack permissions, which is out of the scope of this guide.

> Regions have been mapped as organizations in the IdM. For avoiding collisions, an organization with the name of every region ending in " FIDASH" has been created. Therefore organizations such as `Spain2 FIDASH` or `Crete FIDASH` do represent regions `Spain` or `Crete`. For setting roles inside organizations, several steps must be carried out:

> > 1. create the region if not yet done
> 2. authorize the region to assign roles on the application. This is done by assigning the role `purchaser` to the region
> 3. switching to the region profile. Next steps are done on the region provile
> 4. add the user as member in the region
> 5. enter to the members configuration
> 6. authorize que user by granting him the desired role in the organization for the application. This is done only with the `InfrastructureOwner` role.

### Make a superuser

Superusers can be created easily with the command `python manage.py createsuperuser`. However, when having activated the widget `python-social-auth`, local user database is no longer used. Therefore, the required steps are:

1. login the platform with the IdM user to be made SuperUser. Please take note of the username assigned to that user, which is not his email. Username can be discovered on Wirecloud navigation bar (whose text is "username / workspace name"), or in the URL path, just after the IP address or domain-name, and before the dashboard name.
2. Open a python shell with the command `python manage.py shell` on the WireCloud installation directory and write the following lines replacing `USERNAME` with the real username:

        from django.contrib.auth.models import User
        user = User.objects.get(username='USERNAME')
        user.is_superuser = True
        user.is_staff = True
        user.save()

### Uploading widgets to the new instance

Each of the developed widgets, and the only one operator, is developed on a specific project inside [fidash]([https://mashup.lab.fiware.org](https://mashup.lab.fiware.org)) organization in GitHub.

Widgets are configured using grunt, which is used for setting up the environment, testing, packaging and, optionally, uploading them to the instance. The default grunt action will package them, so leaving the `.wgt` file on the `dist` folder. More detailed instructions can be found on the [developer guide](../developer/developer_guide.md), and indivitual compilation instructions are described in the `README.md` file of each widget.

#### Uploading widgets automatically

The grunt `wirecloud` action will upload the widget and will set it as public to every user in the WireCloud instance. This action will require the URL of the instance and user credentials for carrying out such actions.

#### Uploading widgets manually

To upload widgets, go to the **My Resources** section, click on **Upload** button and then drag all the desired widgets.

To make a widget public, open the Django Admin Console (it must be done through a superadmin user), click on `Catalogue Resources`, enter the desired resource and set on the tick on "Available to all users".

![Access to My Resources](images/my-resources.png) ![upload button](images/upload.png)

