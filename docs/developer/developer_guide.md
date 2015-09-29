# FIDASH Developer Guide

[FIDASH](https://github.com/fidash/fiware-fidash) is an administration and management dashboard for FIWARE Lab. It is derived from [WireCloud](http://conwet.fi.upm.es/wirecloud/) and this allows to inherit the composable mashup environment into which new *widget* can be deployed and instantiated.

## Widget structure

A *widget* is composed by one or more HTML files, JavaScript and CSS files referenced in the HTML, and a config.xml file.

```
├── config.xml
├── index.html
├── css
├── js
├── lib
│   ├── css
│   ├── fonts
│   ├── images
│   └── js
└── manifest.json
```

* The HTML provides the structure for the user interface.
* CSS handles the style.
* JavaScript controls widget's logic. This includes the register of wiring and preferences callbacks.
* config.xml file contains widget metadata (description, author, version etc.)  is written in [Mashable application component Definition Language (MACDL)](https://forge.fiware.org/plugins/mediawiki/wiki/fiware/index.php/FIWARE.ArchitectureDescription.Apps.ApplicationMashup#Mashable_application_component_Definition_Language_.28MACDL.29). The following example shows how to declare a boolean preference named *id* and a wiring output endpoint named *image_id* in [config.xml](https://github.com/fidash/*widget*-listimages/blob/master/src/config.xml):
    * Preferences:

    ```xml
    <preferences>
        <preference name="id" type="boolean" description="Activate to display the id column" label="ID" default="false" />
    </preferences>
   ```
    * Wiring:

    ```xml
    <wiring>
        <outputendpoint name="image_id" type="text" label="Image ID" description="Sends the image ID and OpenStack access." friendcode="image_id"/>
    </wiring>
    ```

For clarity purposes JavaScript and CSS files, as well as third party libraries, should be placed in separate folders. All these files must be uploaded to FIDASH packaged in a `.wgt` file so all library and used resources must be included in the package file or be available on-line.

Once deployed in FIDASH each widget is placed in a separated `iframe` so any communication between each others can only be made through the wiring system provided by FIDASH. Widgets can also communicate with external servers and APIs.

## Widget communication

Wiring is FIDASH's widget connection system. It has two kinds of endpoints, input and output.

Widgets with an input endpoint need to register a callback defining the widget's behavior when an event is received through that endpoint. In order to do this a callback must be passed as an argument to the `wiring.registerCallback` function:

```javascript
MashupPlatform.wiring.registerCallback(endpointName, callback);
```
* `endpointName` is the name defined for the input endpoint in the config.xml file.
* `callback` is a function that defines the behavior of the widget when a wiring event is received through this endpoint.

Widgets with an output endpoint can send data through the wiring connection using the `wiring.pushEvent` function:

```javascript
MashupPlatform.wiring.pushEvent(endpointName, data);
```
* `endpointName` is the name defined for the output endpoint in the config.xml file.
* `data` is the information sent with the event.


## Widget preferences

Each FIDASH widget has its own set of preferences that the developer can set in the config.xml file. It is also possible to listen to changes in these preferences by registering a callback that defines the behavior of the widget in case of a change in a preference value. To register said callback use the `prefs.registerCalback` function:

```javascript
MashupPlatform.prefs.registerCalback(callback);
```
* `callback` is a function defining the behavior of the widget in case of a change in at least one of the values of the preferences.

Notice that this function registers a general callback for every preference defined. There is another function to read a preference:

```javascript
MashupPlatform.prefs.get(prefName);
```
where `prefName` is the name of the preference as defined in the config.xml file.

For further information about **wiring** and **preferences** please look at [widget API](http://conwet.fi.upm.es/wirecloud/widgetapi).


## JStack

[JStack](https://github.com/ging/jstack) is a JavaScript binding for the OpenStack API.

The library is split in submodules for each one of the OpenStack services which allows different namespaces for every service.

When using JStack in a widget the first step must always be initialize the authentication URL:

```javascript
JSTACK.Keystone.init(authURL);
```
where `authURL` is the URL address where the Keystone server is located.

The second step of the process is the authentication. This call will not be done through JStack but through FIDASH's proxy with the following call:

```javascript
var headersAuth = {
    "X-FI-WARE-OAuth-Token": "true",
    "X-FI-WARE-OAuth-Token-Body-Pattern": "%fiware_token%",
    "Accept": "application/json"
};

var authBody = {
    "auth": {
        "identity": {
            "methods": [
                "oauth2"
            ],
            "oauth2": {
                "access_token_id": "%fiware_token%"
            }
        }
    }
};

MashupPlatform.http.makeRequest(authURL + 'tokens', {
    method: 'POST',
    requestHeaders: headersAuth,
    contentType: "application/json",
    postBody: JSON.stringify(authBody),
    onSuccess: success,
    onFailure: error
});
```
This will request a service token to the Keystone server using FIDASH's token as authentication. This FIDASH token will be added to the request by FIDASH's proxy.

The success callback must set JStack state to authenticated and provide the received information to JStack:

```javascript
function success (tokenResponse) {

    var token = tokenResponse.getHeader('x-subject-token');
    var responseBody = JSON.parse(tokenResponse.responseText);

    // Temporal change to fix catalog name
    responseBody.token.serviceCatalog = responseBody.token.catalog;

    // Mimic JSTACK.Keystone.authenticate behavior on success
    JSTACK.Keystone.params.token = token;
    JSTACK.Keystone.params.access = responseBody.token;
    JSTACK.Keystone.params.currentstate = 2;

}
```
Now JStack is ready to make request to the OpenStack API services. For example a request to get a list with all images would be:

```javascript
JSTACK.Nova.getimagelist(detailed, success, error, region);
```
where `detailed` is a boolean set to true to receive all the images attributes and `region` is chosen by the user in the interface.

The response to this request will be a JSON object containing the images list (this example is shortened for brevity's sake):

```json
{  
  "images":[  
    {  
      "status":"active",
      "name":"RealVirtualInteractionGE-3.3.3",
      "deleted":false,
      "container_format":"bare",
      "created_at":"2015-01-15T17:34:20",
      "disk_format":"qcow2",
      "updated_at":"2015-01-15T17:38:21",
      "properties":{  
        "type":"fiware:userinterface",
        "nid":"1310"
      },
      "min_disk":0,
      "protected":false,
      "id":"2b374ea6-c612-450d-91b7-17612fe4bbaa",
      "checksum":"6b1b130a5632168095792c99c6a25bb9",
      "owner":"00000000000000000000000000000001",
      "is_public":true,
      "deleted_at":null,
      "min_ram":0,
      "size":3767730176,
      "region": "Prague"
    },
    "..."
  ]
}
```

## Development tools

### Grunt

Grunt is a JavaScript task runner. Its use is recommended when developing widget since it lets you automate very useful tasks. Some examples of useful grunt tasks are:

* [Copy](https://www.npmjs.com/package/grunt-contrib-copy): This task automatizes the copying of files into the location in which they are going to be when the widget is built. For example, if bootstrap files are in the `node_modules/bootstrap` folder they could be copied to a more appropriate location for later creation of the  widget package.
* [Compress](https://www.npmjs.com/package/grunt-contrib-compress): Once all needed files are copied to the `target` folder this task can compress all he contents of this folder creating the widget package `.wgt`.
* [Replace](https://www.npmjs.com/package/grunt-text-replace): This task replaces a given string or pattern with another in one or more files. It is useful to change the widget version automatically in all files just by changing it in the `package.json` for example.
* [JSHint](https://www.npmjs.com/package/grunt-contrib-jshint): This task runs code style checks for the JavaScript code. An example of .jshintrc configuration file can be found [here](https://github.com/fidash/*widget*-listimages/blob/master/.jshintrc).
* [Clean](https://www.npmjs.com/package/grunt-contrib-clean): This task cleans files and folders and can be useful to clean the `target` file.
* [WireCloud](https://www.npmjs.com/package/grunt-wirecloud): This task automatizes the widget upload process. Notice that if the widget already exist in FIDASH, using this task will be inconsequential.

A complete Gruntfile example can be found [here](https://github.com/fidash/*widget*-listimages/blob/master/Gruntfile.js).

### Unit testing

Karma and Jasmine (or any other JavaScript testing framework) are used for unit testing of the widget's javascript code.

* [Karma](http://karma-runner.github.io/0.13/index.html) is a JavaScript test runner. The karma configuration file lets you specify test files, libraries used, source code, etc. An example of a karma configuration file can be found [here](https://github.com/fidash/*widget*-listimages/blob/master/karma.conf.js). Karma can be run through the [karma grunt task](https://www.npmjs.com/package/grunt-karma).

Since Karma is testing framework agnostic it can be used along with any other JavaScript testing framework like [Jasmine](http://jasmine.github.io/) or [Mocha](https://mochajs.org/).


## Project structure example

The structure explained in this section should not be taken as mandatory since there are many other valid ways to structure a FIDASH [widget](https://github.com/fidash/widget-listimages).

The root folder will contain all configuration files (karma, jshint, grunt, etc.) along with the project's documentation, license and package.json file. The root will contain initially one folder, the `src` folder, but two others could be created along the development process: `node_modules` and `build`.

```
├── build
│   ├── coverage
│   ├── helpers
│   ├── test-reports
│   └── wgt
├── node_modules
│   ├── bootstrap
│   └── jquery
└── src
    ├── css
    ├── js
    ├── lib
    └── test
```

* The `src` folder contains the HTML file(s) and the different folders containing JavaScript code, CSS files and test specs.
* The `node_modules` folder contains every package installed via NPM (e.g. Bootstrap or JQuery).
* The `build` folder contains the packaged widget (.wgt file) and three other folders:
    * `test-reports`: contains the result of the tests.
    * `wgt`: contains all the widget files with the same structure as the packaged widget
    * `coverage`: contains the coverage results of the tests.
