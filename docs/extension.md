# Extension

!> **Note to the Reader** The Extension model has changed significantly from iAccess version 1 to version 2. This section describes key parts of the iAccess 2 extension facilities. However, it is not complete and should be considered *Work in Progress*. If you are unable to find what you are looking for here, we recommend posting a question to the Engineering team through our "iAccess for Maconomy" Kona space (https://www.kona.com/#!/projects/129727). We will reply there and take note of your questions, feedback, and comments for future iterations of this section.

This section describes how to make client-side iAccess extensions using built-in extension facilities as well as tooling provided by the Maconomy Extender. Client-side extensions cover authentication methods, preferred settings, menu customization, and updates to existing workspaces/addition of new workspaces. The primary goal of iAccess extensions is to customize the appearance of Maconomy functionality when leveraged over a Web user interface. If you need to make fundamental changes such as extending core business logic and adding new fields and actions, use the Java extension framework to create server-side extensions. While the two extension approaches can be used together, it is important to note that the purpose of client-side extensions is to change how Maconomy functionality is rendered, not how it works.

The iAccess runtime is essentially version-independent. It runs on different Maconomy backends and service pack ranges. On the other hand, the iAccess applications are tied to specific Maconomy backends or applications (that is, Application Packaging Units or *APUs*). If you install a specific iAccess FPU, it will look and act differently depending on which Maconomy version you are running in the backend. This approach is necessary since different Maconomy versions expose different containers, fields, actions, system parameters, and backend extension capabilities.

When developing new iAccess extensions or upgrading existing ones, you must take note of what the target Maconomy backend is because this restricts what containers, actions, fields, and so on, are available. The iAccess FPU contains different applications, each compatible with a specific range of service packs on a given major Maconomy version. You must also look at the iAccess API version that the given iAccess FPU exposes. The API version determines the kinds of extension possibilities available and their properties.

Both the iAccess application version and the API version are specified in the root of the iAccess configuration files, specifically in the `application.json` file. In the following example, the iAccess application is called `17` and the current version is `1.0.2`. The FPU manifest describes the backend Maconomy versions compatible with this application. This sample configuration complies with version `8.0.0` of the iAccess runtime API.

    {
      "api": "8.0.0",
      "application": {
        "name": "17",
        "version": "1.0.2"
      },
      "authentication": {
        "$ref": "Authentication:Authentication"
      },
      "platform": {
        "$ref": "Platform:Platform"
      },
      "shell": {
        "$ref": "Shell:Shell"
      },
      "workspace": {
        "$ref": "Workspace:Workspace"
      }
    }

The remainder of this file consists of JSON references to the four main iAccess areas:

* Authentication - Configuration of available and preferred login methods.
* Platform - Configuration and tweaking of low-level iAccess runtime mechanics.
* Shell - Configuration of the sidebar menu, notifications, and preferences.
* Workspace - Configuration of workspaces and their layouts.

The following subsections describe these areas in greater detail.

#### A Note about iAccess Configuration Files

iAccess configurations use the JSON format, a standard notation similar to XML. During runtime, iAccess requests a single configuration file describing all extensions (standard or custom). This file is called `application.json` and is retrieved through the `configurations` end point in the REST API. In the iAccess source configuration files, the notation (see the following example)

    {
      "$ref": "Authentication:Authentication"
    }

is a heavily used modularization technique. The JSON object is replaced (or macro expanded) by the `Authentication.json` configuration file located in the `Authentication` folder.

When the iAccess configuration files are processed by the REST API, all JSON properties with the prefix `T$` are translated to the language utilized by the end-user. For example, if an iAccess source configuration file has the following contents:

    {
        "T$title": "Hello World"
    }

then a Spanish user receives the following content in his/her browser:

    {
        "title": "Hola mundo"
    }

The translation relies on standard Maconomy dictionaries. It only works if a dictionary containing the required terms exists in the chosen language.

## Authentication

The *authentication* part is the first main area of iAccess extension. It specifies the authentication methods available to end-users when they log in to iAccess. How you configure authentication determines the screen end-users see when they first visit the iAccess web page. For a sample configuration, refer to the following text:

    {
      "preferred": "maconomy",
      "methods": {
        "maconomy": {
          "enabled": true
        },
        "domain": {
          "enabled": true
        },
        "sso": {
          "enabled": true
        },
        "azure": {
          "enabled": true
        }
      }
    }

Although this is probably the simplest area in terms of iAccess configuration, authentication is often hard to get right in actual installations. As an installation consultant, you must focus on setting up the right infrastructure and specifying a corresponding *preferred* authentication method. The preferred method determines how iAccess will redirect the browser for the user accessing the root URL (for example: `/`) If you specify *maconomy* as preferred, iAccess will redirect the browser to the `/maconomy` URL so the user can enter login credentials there.

iAccess currently supports four different authentication methods:

Maconomy
: A standard Maconomy login page where the user can enter his/her username and password.

Domain
: A domain login page where the user can enter domain, username, and password.

SSO
: Single Sign-On using Kerberos authentication and the SPNEGO protocol [@rfc4178; @rfc4559] which takes the user past the login screen and directly into the application. If the login fails, the user is redirected to the domain login page as a fallback.

Azure
: Single Sign-On using Azure which takes the user through the Azure login flow. This flow varies depending on the customer's setup. To force account selection during the Azure login flow, the user can opt to append `prompt=select_account` to the iAccess URL as an extra query parameter.

If you disable an authentication method, you also disable the iAccess URL associated with that login method. Deltek recommends that only required authentication methods are left enabled on production installations.

#### Subcontractor Login

It makes sense for a company with different types of users sharing an iAccess installation to employ more than one authentication method. For example, a company with domain login configured for its employees will need a different method for subcontractors who are not allowed on the domain. In this case, the company can provide Maconomy credentials for its subcontractors. The company can then choose domain login as its preferred authentication method on the system, but instruct its subcontractors to log in to iAccess using the `/maconomy` URL which leads directly to the Maconomy login page. The suggested configuration for this is as follows:

    {
      "preferred": "domain",
      "methods": {
        "maconomy": {
          "enabled": true
        },
        "domain": {
          "enabled": true
        },
        "sso": {
          "enabled": false
        },
        "azure": {
          "enabled": false
        }
      }
    }

## Platform

The second main area of iAccess extension is the *platform* part which specifies various low-level iAccess behaviors. You can find the default configuration of the platform part in the `Platform.json` file:

    {
      "usageTracking": {
        "$ref": "Usagetracking"
      },
      "containers": {
        "$ref": "Containers"
      },
      "typeAhead": {
        "$ref": "Typeahead"
      }
    }

#### Usage Tracking

The *usage tracking* part concerns the integration between iAccess and Google Analytics. This feature was also present in iAccess version 1 and is used to track page views, events, errors, and other usage data about end-users. You can acquire your own tracking ID directly from Google, and add it to the configuration so you can collect usage data about an iAccess installation. In the following excerpt, the Google Analytics tracking ID `UA-123456789-1` is added to the standard configuration:

    {
      "enabled": true,
      "endUserOptIn": true,
      "trackingId": "UA-123456789-1"
    }

The two mandatory properties, `enabled` and `enduserOptIn`, are used to (1) enable/disable tracking completely and (2) show/hide the cookie consent banner. If tracking is disabled, then iAccess still creates cookies in the browser but performs no actual tracking. If the end-user opt-in is disabled, then users are not presented with a banner informing them of tracking.

#### Containers

The *containers* part is active and is a new feature introduced in iAccess version 2. The containers configuration allows consultants to supply additional metadata about REST API containers. This is necessary because the specification of containers that we get through the `containers` endpoint only describes a subset of the semantics of the backend. The configuration format follows a very simple convention: it is an object with properties matching the container names from the REST API. You can add information about each container's various aspects, and the iAccess runtime will then adapt to this new data.

##### Singleton Containers

Maconomy makes a special distinction between normal and *singleton* containers. Whereas normal containers represent collections of resources, singleton containers always represent a single resource. This leads to a slightly different navigation interface in the REST API. Only very few containers are singletons, and these are not specifically identified by the REST API. However, since some of these are very prominent for most users, iAccess allows the consultant to add information about singletons in the containers configuration.

    {
      "TimeRegistration": {
        "card": {
          "singleton": {
            "DateVar": "card.datevar",
            "EmployeeNumberVar": "card.employeenumbervar"
          }
        }
      }
    }

The preceding excerpt specifies *TimeRegistration* as a singleton container. *DateVar* and *EmployeeNumberVar* are used when navigating with this container. Singleton properties on the right side refer to internal names used by the REST API when navigating this container.

##### File Actions

Another feature of the containers configuration is the ability to add information about file actions. The REST API supports actions for uploading files. However, it does not specify which ones are actually file actions. This information is important since the protocols for dealing with file actions are different from those for normal actions, both in the iAccess runtime and in terms of messages exchanged between the browser and the REST API.

    {
      "ExpenseSheets": {
        "card": {
          "actions": {
            "AttachDocument": {
              "attachments": {
                "required": true,
                "allowMultipleAttachments": true
              }
            }
          }
        },
        "table": {
          "actions": {
            "AttachDocumentToLine": {
              "attachments": {
                "required": true,
                "allowMultipleAttachments": false
              }
            }
          }
        }
      }
    }

The preceding configuration specifies that the *AttachDocument* action on the *ExpenseSheets* card pane and the *AttachDocumentToLine* action on the corresponding table pane are file actions. Both require an attached file, but they differ in the number of files they allow as attachments.

##### Action Parameters

Some Maconomy actions require certain variables to have a particular value when executed. The REST API does not specify these variables, so iAccess can add this information as so-called *parameters* in the container configuration. In the following example, the *ApproveAbsenceEntry* action on the card pane of the *AbsenceEntryOverview* container is configured to require four variables as parameters, namely: *EntryDateVar*, *ValidTillVar*, *NumberOfDaysVar*, and *ReasonVar*.

    "AbsenceEntryOverview": {
      "card": {
        "actions": {
          "ApproveAbsenceEntry": {
            "parameters": {
              "EntryDateVar": "card.entrydatevar",
              "ValidTillVar": "card.validtillvar",
              "NumberOfDaysVar": "card.numberofdaysvar",
              "ReasonVar": "card.reasonvar"
            }
          }
        }
      }
    }

##### Filter-As-Table Panes

Standard Maconomy containers have at least one of the following pane types: card, table, and filter. iAccess 2 includes a new special type called *Filter as Table* which is handled purely on the client-side. This pane type allows consultants to render a standard filter pane as a table pane. In general, filters are read-only whereas tables are editable. When using a filter as a table, the currently selected record is actually the corresponding card pane record. This makes the filter appear as an editable table, although it takes a bit longer to respond since iAccess has to load the corresponding card record whenever the user selects a filter row.

    "AbsenceEntryOverview": {
      "filterAsTable": {
        "fields": {
          "RelatedEntryValidTill": {
            "immutable": true
          },
          "EmployeeName1": {
            "mapsTo": "EmployeeNameVar"
          }
        }
      }
    }

To make a filter pane available as a table, you may need to add additional field specifications in the containers configuration file. In the preceding example, two changes are added. First, the *RelatedEntryValidTill* field is specified as immutable. This is a performance optimization which states that this field will not change its value when its card record is edited. This means that iAccess does not to need to reread the field when a user edits the card record. Second, the *EmployeeName1* field is mapped to the *EmployeeNameVar* field. This is necessary in cases where an underlying database column has different field names depending on whether it is shown in the filter or in the card. The `mapsTo` attribute allows iAccess to link these two fields.

##### Configuration Attributes for Controlling Caching of New Record Data

When a new card or table record is created, iAccess sends a request to the server to obtain default values for the new record. By default, these values are cached for all containers. iAccess 2.4.1 introduces a configuration setting that you can use to disable caching for a specific container.

For example, to disable caching of new record data for both the card and the table panes of the ExpenseSheets container, add the following attributes to the Containers.json file:

```
{
  "ExpenseSheets": {
    "card": {
      "cacheInitResponse": false,
      ...
    },
    "table": {
      "cacheInitResponse": false,
      ...
    }
  },
  ...
}
```

#### Type Ahead

Type Ahead is a feature available in table panes which lets the user perform changes, such as adding, editing and deleting lines, or running line actions, without having to wait for a server response after each action. The requested changes are queued and executed in the background.

In some cases, it might be desirable to disable this functionality, or to control how many uncommitted changes a user is able to make. This can be configured using the attributes available in the Typeahead.json file.

## Shell

The *shell* part is the third main area of iAccess extension, and this refers to the part of the application that surrounds the workspace area after the user logs in. The core configuration covers the sidebar menu as well as the documentation URL, settings, and notifications in the top-right corner.

    {
      "menu": {
        "$ref": "Menu"
      },
      "documentationUrl": "https://help.deltek.com/Product/MaconomyiAccess/<version>",
      "settings": {
        "$ref": "Settings"
      },
      "notifications": {
        "$ref": "Notifications"
      }
    }

### Menu

The sidebar menu is configured in the `Menu.json` file. [The *workspace* part of the iAccess configuration](#workspace) contains the total list of available workspaces. The menu is a subset of these workspaces, ordered in groups. There is no limit to the number of groups nor the number of workspaces within a group. iAccess does not allow the use of nested groups, so avoid adding too many groups and workspaces to the menu. Doing so clutters the user interface and makes navigation difficult for the user.

    {
      "groups": [
        {
          "T$title": "Self Service",
          "items": [
            {
              "workspace": "WeeklyTimeSheets"
            },
            ...
          ]
        },
        ...
      ]
    }

Groups have a `title` property and a list of items. Each item represents either a concrete workspace or a hyperlink. You can assign a title to a specific workspace. The `workspace` property refers to the internal name of the workspace as declared in [the *workspace* part of the iAccess configuration](#workspace). On the other hand, hyperlinks are composed of a title and a URL. Placing hyperlinks in the menu is convenient if access to third-party systems is required.

Groups, workspaces, and hyperlinks have an optional `visible` property which determines their visibility. To specify this property, you must use an expression. The following example shows an excerpt of a menu where the *Employee Information* workspace is only visible to users with either the Project Manager or HR Manager role. When specifying a role name.

    {
      "T$title": "Employee Information",
      "workspace": "EmployeeInformation"
      "visible": "hasRole('ProjectManager', 'HRManager')"
    }


### Documentation URL

The documentation URL is a simple hyperlink to external documentation. It is rendered as a question mark in the top-right corner of the screen. By default, it points to the standard hosted help from Deltek. It is version-specific because the `<version>` placeholder is substituted with the iAccess version at runtime. Customers who prefer to use their own external documentation (such as a page on an internal Sharepoint site) can simply replace the URL here.

### Settings

Settings concern iAccess language and formatting. Select the language used in iAccess from the dictionaries installed on the Maconomy server. To further filter the server list of languages, you can use the `couplingconfiguration.mcsl.xml` file found in the 'Definitions' folder on the server.

Aside from specifying the preferred language, you need to configure the `fixed` flag which states whether the user can change the language used. If you set the fixed flag to 'false', the user can change the language on the login screen and in the settings dialog inside iAccess. If you set the fixed flag to 'true', make sure the preferred language is actually available from the server. In other words, the iAccess language configuration must be aligned with the set of dictionaries installed on the server and with any filters defined in the *MCSL* specification.

Default data formatting is location-specific. This format controls rendering of dates, as well as the decimal separator and digit grouping used. You can edit the preferred location and the settings for that location. You also have the option to assign formatting to a specific location by using the `fixed` property. The following example shows the `preferred` and `fixed` properties in use, as well as a single location configured with a date format, a decimal separator, and a digit grouping system.

    {
      "preferred": "da_DK",
      "fixed": false,
      "available": {
        "da_DK": {
          "date": {
            "short": "dd/MM/y"
          },
          "symbol": {
            "decimal": ",",
            "group": "."
          }
        },
        ...
      }
    }

You can also configure the optional `minutesThreshold` property, which determines whether a time entry is interpreted as minutes or hours. The default value is '10', which means that an entry of '10' is interpreted as 10 minutes, and an entry of '11' is interpreted as 11 hours.

### Notifications

Use the `recalculation` object to configure how often iAccess retrieves the notifications computed on the server. Specifically, you can use the `interval` property to configure how often iAccess should request the recalculation of a specific user's notifications. You can also set the `initialDelay` property to configure when iAccess should start the recalculation after the user logs in. Both of these properties are specified in minutes. If you make the recalculation interval too short, you risk causing a serious system-wide performance degradation.

    {
      "recalculation": {
        "initialDelay": 30,
        "interval": 30
      }
    }

### Customization Procedures

#### Create a Menu Group

You can create a menu group, and move specific menu items into this group.

__To create a menu group:__

1. In the __Standard and Solution Files Filter Search__ field, type the Menu.json filename.
   You can also specify the file path (that is: Web >> iaccess >> [iAccess version] >> shell >> menu.json).

2. In the search results, double-click the Menu.json file for the iAccess version you want to customize.
   The Extender opens the Menu.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the Menu.json file, look for the "groups" property. You create menu groups under this property.
   For example, if you want to create a menu group for workspaces used by Time and Expense users, edit the code as follows:


From


    {
      "groups": [
        {
          "T$title": "Self Service",
          "items": [
            {
              "T$title": "Weekly Time Sheet",
              "workspace": "WeeklyTimeSheets"
            },
        ...
          ]
        },


To


    {
      "groups": [
        {
          "T$title": "Time & Expense",
          "items": [

          ]
        }
        {
          "T$title": "Self Service",
          "items": [
            {
              "T$title": "Weekly Time Sheet",
              "workspace": "WeeklyTimeSheets"
            },
        ...
          ]
        },


5. Select the code for all the workspaces you want to move into the new group. Make sure you include the braces for each workspace object.

        {
          "T$title": "Weekly Time Sheet",
          "workspace": "WeeklyTimeSheets"
        },

   For this example, select the code for the following workspaces: Weekly Time Sheets, Daily Time Sheets, Expenses, Mileage, Favorites, Absence, and Purchase Orders.

6. Cut and paste the selected code inside the brackets of the "items" property in the new menu group you created.


For this example, the code for the new menu group should now read:


     {
       "groups": [
         {
           "T$title": "Time & Expense",
           "items": [
             {
               "T$title": "Weekly Time Sheet",
               "workspace": "WeeklyTimeSheets"
             },
             {
               "T$title": "Daily Time Sheet",
               "workspace": "DailyTimeSheets"
             },
             {
               "T$title": "Expenses",
               "workspace": "ExpenseSheets"
             },
             {
               "T$title": "Mileage",
               "workspace": "MileageSheets"
             },
             {
               "T$title": "Favorites",
               "workspace": "Favorites"
             },
             {
               "T$title": "Absence",
               "workspace": "Absence"
             },
             {
               "T$title": "Purchase Orders",
               "workspace": "PurchaseOrders"
             }
           ]
         }
       ]
     }


7. Click the __Save__ icon.

8. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

9. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

10. In the Deployment success message that displays, click __OK__.

11. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.

#### Restrict Access to a Menu Group

You can restrict access to a menu group such that it is only visible to users with specific roles.

__To restrict access to a menu group:__

1. In the __Standard and Solution Files Filter Search__ field, type the Menu.json filename.
   You can also specify the file path (that is: Web >> iaccess >> [iAccess version] >> shell >> menu.json).

2. In the search results, double-click the Menu.json file for the iAccess version you want to customize.
   The Extender opens the Menu.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the Menu.json file, scroll down to the menu group to which you want to restrict access.

5. Add a visible property to this menu group.
   For example, if you want to restrict access to a newly created Time and Expense menu group such that only users assigned to specific roles can view the workspaces under the group, edit the code as follows:


From


    "groups": [
     {
       "T$title": "Time & Expense",
       "items": [
        {
           "T$title": "Weekly Time Sheet",
           "workspace": "WeeklyTimeSheets"
        },


To


    "groups": [
     {
       "T$title": "Time & Expense",
       "visible": "hasRole('iAccess T&E', 'iAccess Manager')",
       "items": [
        {
           "T$title": "Weekly Time Sheet",
           "workspace": "WeeklyTimeSheets"
        },


   __Note:__ Roles refer to window groups you set up in the Workspace Client.

6. Click the __Save__ icon.

7. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

8. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

9. In the Deployment success message that displays, click __OK__.

10. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Log out, then log in again.

#### Remove a Menu Item

__To remove a menu item:__

1. In the __Standard and Solution Files Filter Search__ field, type the Menu.json filename.
   You can also specify the file path (that is: Web >> iaccess >> [iAccess version] >> shell >> menu.json).

2. In the search results, double-click the Menu.json file for the iAccess version you want to customize.
   The Extender opens the Menu.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the Menu.json file, delete the workspace from the list. Make sure you also delete the braces before and after the workspace object.

   For example, if you want to remove the Weekly Time Sheets menu item, edit the code as follows:


From


    "T$title": "Self Service",
    "items": [
      {
        "workspace": "WeeklyTimeSheets"
      },
      {
        "workspace": "DailyTimeSheets"
      },


To


    "T$title": "Self Service",
    "items": [
      {
        "workspace": "DailyTimeSheets"
      },


5. Click the __Save__ icon.

6. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

7. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

8. In the Deployment success message that displays, click __OK__.

9. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.


#### Rename a Menu Item

__To rename a menu item:__

1. In the __Standard and Solution Files Filter Search__ field, type the Menu.json filename.
   You can also specify the file path (that is: Web >> iaccess >> [iAccess version] >> shell >> menu.json).

2. In the search results, double-click the Menu.json file for the iAccess version you want to customize.
   The Extender opens the Menu.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the Menu.json file, add a "T$title" property to the workspace object you want to rename.
   For example, if you want to change the name of the Employee Information workspace to "Employee Info", edit the code as follows:


From


    {
     "workspace": "EmployeeSelfService"
    },
    {
     "workspace": "EmployeeInformation"
    },


To


    {
     "workspace": "EmployeeSelfService"
    },
    {
     "T$title": "Employee Info",
     "workspace": "EmployeeInformation"
    },


5. Click the __Save__ icon.

6. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

7. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

8. In the Deployment success message that displays, click __OK__.

9. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.



#### Customize a Search Filter Name

You can rename the search filters found in some workspaces.

__To customize a search filter name:__

1. In the __Standard and Solution Files Filter Search__ field, type the name of the heading.json file for the workspace that you want to customize.
   You can also specify the file path.
   For example, if you want to rename the __My Open__ search filter found in the Expenses workspace, search for the ExpenseSheets_Heading.json file, or specify the following file path: Web >> iaccess >> [iAccess version] >> workspace >> EmployeeSelfService >> ExpenseSheets >> ExpenseSheets_Heading.json.

2. In the search results, double-click the heading.json file for the iAccess version you want to customize.
   The Extender opens the heading.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the heading.json file, scroll to the "selection" property. Under this, the "options" property lists the available search filters for a workspace.

5. Edit the "T$title" property for the search filter you want to rename.
   For example, if you want to rename the __My Open__ search filter, edit the code as follows:


From


    "options": {
      "MyOpenExpenseSheets": {
        "T$title": "My Open",
        "restriction": "not FullyApproved and EmployeeNumber = employeeNumber()"
      }


To


    "options": {
      "MyOpenExpenseSheets": {
        "T$title": "My Open Expenses",
        "restriction": "not FullyApproved and EmployeeNumber = employeeNumber()"
      }


6. Click the __Save__ icon.

7. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

8. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

9. In the Deployment success message that displays, click __OK__.

10. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.


## Workspace

The *workspace* part is the fourth main area of iAccess extension. It specifies the structure and layout for all workspaces available in iAccess. This part represents the majority of iAccess extension capabilities, since end-users spend most of their time in the workspaces. It has two components: a set of workspaces, and a set of global definitions.

    {
      "workspaces": {
        "Absence": {
          "$ref": "EmployeeSelfService:AbsenceMgmt"
        },
        ...
      },
      "definitions": {
        "$ref": "GlobalDefinitions"
      }
    }

In the `Workspace.json` file (as shown in the preceding example), the `workspaces` property is a map of all embedded workspaces, and includes the entire collection of workspaces. The sidebar menu is a subset of this collection.

The `definitions` property specifies a set of named styles that can be used across workspaces.

Each workspace has a unique name that serves as its internal identifier and an external, localizable title. The contents of a workspace has two main parts: the data bindings and the layout (as shown in the following example). The data bindings is a configuration of the Maconomy containers that provide data for the workspace. These containers are bound together in a tree, similar to how workspace definitions (*MWSL* specifications) are done for the Workspace Client. On the other hand, the layout is a configuration of how this tree of Maconomy containers is rendered to the end-user. This corresponds roughly to dialog layouts (*MDML* specifications) for the Workspace Client. The following subsections discuss data bindings and layouts in greater detail.

    {
      "name": "ExpenseSheets",
      "T$title": "Expenses",
      "dataBindings": {
        ...
      },
      "layout": {
        ...
      }
    }

#### Data Bindings

Copy to come.

#### Layouts

Copy to come.

#### Wizards

Copy to come.

#### Customization Procedures

##### Rename a Card Action

iAccess has several actions available in the card part of each workspace. You can customize the names of most of these actions.

__To rename a card action:__

1. In the __Standard and Solution Files Filter Search__ field, type the name of the ActionBar.json file that corresponds to the workspace you want to customize.
   You can also specify the file path.
   For example, if you want to rename the __Submit__ action in the card part of the Expenses workspace, search for the ExpenseSheets_ActionBar.json file, or specify the following file path: Web >> iaccess >> [iAccess version] >> workspace >> EmployeeSelfService >> ExpenseSheets >> ExpenseSheets_ActionBar.json.

2. In the search results, double-click the ActionBar.json file for the iAccess version you want to customize.
   The Extender opens the ActionBar.json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the ActionBar.json file, scroll to the instance of the "actions" property that contains the action you want to rename. This property lists the actions that you are allowed to customize.

5. Edit the "T$title" property for the action you want to rename.
   For example, if you want to rename the __Submit__ action, edit the code as follows:


From


    "actions": [
     {
       "T$title": "Submit",
       "source": "SubmitExpenseSheet"
     },


To


    "actions": [
     {
       "T$title": "Submit My Expense",
       "source": "SubmitExpenseSheet"
     },


6. Click the __Save__ icon.

7. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

8. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

9. In the Deployment success message that displays, click __OK__.

10. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.

##### Rename a Field

__To rename a field:__

1. In the __Standard and Solution Files Filter Search__ field, type the name of .json file for the part of the workspace that contains the field you want to rename.
   You can also specify the file path.
   For example, if you want to rename the __Total Amount__ field found in the card part of the Expenses workspace, search for the ExpenseSheets_Card_Row.json file, or specify the following file path: Web >> iaccess >> [iAccess version] >> workspace >> EmployeeSelfService >> ExpenseSheets >> ExpenseSheets_Card_Row.json.

2. In the search results, double-click the .json file for the iAccess version you want to customize.
   The Extender opens the .json file.

3. Click the __Copy selected file as extension to active project__ icon.

4. In the .json file, scroll down to the "column" property for the column that contains the field you want to rename.

5. Edit the "T$title" property for the field you want to rename.
   For example, to change the name of the __Total Amount__ field to __Full Amount__, edit the code as follows:


From


    "unitField": {
      "T$title": "Total Amount",
      "source": "AmountBase",


To


    "unitField": {
      "T$title": "Full Amount",
      "source": "AmountBase",


6. Click the __Save__ icon.

7. To deploy your changes, click the __Commit and Push changes to Server Repository__ icon.

8. In the window that displays:

    a.	Fill out the __Commit message__ field with the details of your customization.
    b.	You can select the __Deploy immediately__ check box.
    c.	Click __OK__.

   The Extender pushes your changes to the server repository, and displays a progress bar.

9. In the Deployment success message that displays, click __OK__.

10. To view your changes:

    a.	Pull up the browser window with your open iAccess system.
    b.	Hold down the CTRL key, and click __Refresh__.

