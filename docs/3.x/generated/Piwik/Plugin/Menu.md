<small>Piwik\Plugin\</small>

Menu
====

Since Piwik 2.4.0

Base class of all plugin menu providers.

Plugins that define their own menu items can extend this class to easily
add new items, to remove or to rename existing items.

Descendants of this class can overwrite any of these methods. Each method will be executed only once per request
and cached for any further menu requests.

For an example, see the [https://github.com/piwik/piwik/blob/master/plugins/ExampleUI/Menu.php](https://github.com/piwik/piwik/blob/master/plugins/ExampleUI/Menu.php) plugin.

Methods
-------

The class defines the following methods:

- [`__construct()`](#__construct)
- [`urlForDefaultAction()`](#urlfordefaultaction) &mdash; Generates a URL for the default action of the plugin controller.
- [`urlForAction()`](#urlforaction) &mdash; Generates a URL for the given action.
- [`urlForDefaultUserParams()`](#urlfordefaultuserparams) &mdash; Returns the &idSite=X&period=Y&date=Z query string fragment, fetched from current logged-in user's preferences.
- [`configureReportingMenu()`](#configurereportingmenu) &mdash; Configures the reporting menu which should only contain links to reports of a specific site such as "Search Engines", "Page Titles" or "Locations & Provider".
- [`configureTopMenu()`](#configuretopmenu) &mdash; Configures the top menu which is supposed to contain analytics related items such as the "All Websites Dashboard".
- [`configureUserMenu()`](#configureusermenu) &mdash; Configures the user menu which is supposed to contain user and help related items such as "User settings", "Alerts" or "Email Reports".
- [`configureAdminMenu()`](#configureadminmenu) &mdash; Configures the admin menu which is supposed to contain only administration related items such as "Websites", "Users" or "Plugin settings".

<a name="__construct" id="__construct"></a>
<a name="__construct" id="__construct"></a>
### `__construct()`

#### Signature


<a name="urlfordefaultaction" id="urlfordefaultaction"></a>
<a name="urlForDefaultAction" id="urlForDefaultAction"></a>
### `urlForDefaultAction()`

Since Piwik 2.7.0

Generates a URL for the default action of the plugin controller.

Example:
```
$menu->addItem('UI Framework', '', $this->urlForDefaultAction(), $orderId = 30);
// will add a menu item that leads to the default action of the plugin controller when a user clicks on it.
// The default action is usually the `index` action - meaning the `index()` method the controller -
// but the default action can be customized within a controller
```

#### Signature

-  It accepts the following parameter(s):
    - `$additionalParams` (`array`) &mdash;
       Optional URL parameters that will be appended to the URL
- It returns a `array` value.

<a name="urlforaction" id="urlforaction"></a>
<a name="urlForAction" id="urlForAction"></a>
### `urlForAction()`

Since Piwik 2.7.0

Generates a URL for the given action.

In your plugin controller you have to create a method with the same name
as this method will be executed when a user clicks on the menu item. If you want to generate a URL for the
action of another module, meaning not your plugin, you should use the method urlForModuleAction().

#### Signature

-  It accepts the following parameter(s):
    - `$controllerAction` (`string`) &mdash;
       The name of the action that should be executed within your controller
    - `$additionalParams` (`array`) &mdash;
       Optional URL parameters that will be appended to the URL
- It returns a `array` value.

<a name="urlfordefaultuserparams" id="urlfordefaultuserparams"></a>
<a name="urlForDefaultUserParams" id="urlForDefaultUserParams"></a>
### `urlForDefaultUserParams()`

Returns the &idSite=X&period=Y&date=Z query string fragment, fetched from current logged-in user's preferences.

#### Signature

-  It accepts the following parameter(s):
    - `$websiteId` (`bool`) &mdash;
      
    - `$defaultPeriod` (`bool`) &mdash;
      
    - `$defaultDate` (`bool`) &mdash;
      

- *Returns:*  `string` &mdash;
    eg '&idSite=1&period=week&date=today'
- It throws one of the following exceptions:
    - [`Exception`](http://php.net/class.Exception) &mdash; in case a website was not specified and a default website id could not be found

<a name="configurereportingmenu" id="configurereportingmenu"></a>
<a name="configureReportingMenu" id="configureReportingMenu"></a>
### `configureReportingMenu()`

Configures the reporting menu which should only contain links to reports of a specific site such as "Search Engines", "Page Titles" or "Locations & Provider".

#### Signature

-  It accepts the following parameter(s):
    - `$menu` ([`MenuReporting`](../../Piwik/Menu/MenuReporting.md)) &mdash;
      
- It does not return anything.

<a name="configuretopmenu" id="configuretopmenu"></a>
<a name="configureTopMenu" id="configureTopMenu"></a>
### `configureTopMenu()`

Configures the top menu which is supposed to contain analytics related items such as the "All Websites Dashboard".

#### Signature

-  It accepts the following parameter(s):
    - `$menu` ([`MenuTop`](../../Piwik/Menu/MenuTop.md)) &mdash;
      
- It does not return anything.

<a name="configureusermenu" id="configureusermenu"></a>
<a name="configureUserMenu" id="configureUserMenu"></a>
### `configureUserMenu()`

Configures the user menu which is supposed to contain user and help related items such as "User settings", "Alerts" or "Email Reports".

#### Signature

-  It accepts the following parameter(s):
    - `$menu` ([`MenuUser`](../../Piwik/Menu/MenuUser.md)) &mdash;
      
- It does not return anything.

<a name="configureadminmenu" id="configureadminmenu"></a>
<a name="configureAdminMenu" id="configureAdminMenu"></a>
### `configureAdminMenu()`

Configures the admin menu which is supposed to contain only administration related items such as "Websites", "Users" or "Plugin settings".

#### Signature

-  It accepts the following parameter(s):
    - `$menu` ([`MenuAdmin`](../../Piwik/Menu/MenuAdmin.md)) &mdash;
      
- It does not return anything.

