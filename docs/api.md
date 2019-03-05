# API Reference

The following section gives an overview of all parts of the configuration API. Each configuration part consists of a JSON object with a set of properties.

## Application :id=type-application

The application name and version.

Properties: [name](#type-application-property-name), [version](#type-application-property-version)

### name :id=type-application-property-name

The name of the application. Usually, the name bears some resemblance to core Maconomy release versions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### version :id=type-application-property-version

The version of this particular application. This version number is NOT related to core Maconomy versions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

## Assign :id=type-assign

No description available

Properties: [field](#type-assign-property-field), [value](#type-assign-property-value)

### field :id=type-assign-property-field

String alias for field source/model names.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### value :id=type-assign-property-value

String alias for an expression.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

## AuthenticationType :id=type-authenticationtype

Representation of available methods of logging in to iAccess.

## Azure :id=type-azure

No description available

Properties: [enabled](#type-azure-property-enabled)

### enabled :id=type-azure-property-enabled

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

## Configuration API :id=type-configuration_api

The core application configuration is split into four main areas: authentication, platform, shell, and workspace. The entire configuration has an API version used to guarantee compatibliity and enforce upgrades. Finally, the configuration includes a dictionary of the static terms embedded in iAccess. These terms are localized before the client receives the configuration from the REST API.

Properties: [api](#type-configuration_api-property-api), [application](#type-configuration_api-property-application), [authentication](#type-configuration_api-property-authentication), [platform](#type-configuration_api-property-platform), [shell](#type-configuration_api-property-shell), [workspace](#type-configuration_api-property-workspace)

### api :id=type-configuration_api-property-api

The version of the configuration format that this representation conforms to. Versions follow the SemVer standard.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### application :id=type-configuration_api-property-application

The application name and version.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Application](#type-application)| true | _n/a_ |

### authentication :id=type-configuration_api-property-authentication

Authentication determines preferred login mechanism as well as general configuration of the login flow.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IAuthenticationConfiguration](#type-iauthenticationconfiguration)| true | _n/a_ |

### platform :id=type-configuration_api-property-platform

General configuration that spans the entire application

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IPlatformConfiguration](#type-iplatformconfiguration)| true | _n/a_ |

### shell :id=type-configuration_api-property-shell

The application shell covers the menu, documentation, notifications and auxiliary features such as settings, change password and about information.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IShellConfiguration](#type-ishellconfiguration)| true | _n/a_ |

### workspace :id=type-configuration_api-property-workspace

Configuration of general properties that span all workspaces as well as configuration of individual workspaces in terms of data bindings and layouts.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IWorkspaceConfiguration](#type-iworkspaceconfiguration)| true | _n/a_ |

## Domain :id=type-domain

No description available

Properties: [enabled](#type-domain-property-enabled)

### enabled :id=type-domain-property-enabled

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

## Formatting :id=type-formatting

Configure formatting rules for data types.

Properties: [amount](#type-formatting-property-amount), [autotimestamp](#type-formatting-property-autotimestamp), [boolean](#type-formatting-property-boolean), [date](#type-formatting-property-date), [enum](#type-formatting-property-enum), [integer](#type-formatting-property-integer), [real](#type-formatting-property-real), [string](#type-formatting-property-string), [time](#type-formatting-property-time), [timeduration](#type-formatting-property-timeduration)

### amount :id=type-formatting-property-amount

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IAmountFormatting](#type-iamountformatting)| false | _n/a_ |

### autotimestamp :id=type-formatting-property-autotimestamp

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IAutoTimestampFormatting](#type-iautotimestampformatting)| false | _n/a_ |

### boolean :id=type-formatting-property-boolean

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IBooleanFormatting](#type-ibooleanformatting)| false | _n/a_ |

### date :id=type-formatting-property-date

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IDateFormatting](#type-idateformatting)| false | _n/a_ |

### enum :id=type-formatting-property-enum

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IEnumFormatting](#type-ienumformatting)| false | _n/a_ |

### integer :id=type-formatting-property-integer

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IIntegerFormatting](#type-iintegerformatting)| false | _n/a_ |

### real :id=type-formatting-property-real

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IRealFormatting](#type-irealformatting)| false | _n/a_ |

### string :id=type-formatting-property-string

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IStringFormatting](#type-istringformatting)| false | _n/a_ |

### time :id=type-formatting-property-time

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ITimeFormatting](#type-itimeformatting)| false | _n/a_ |

### timeduration :id=type-formatting-property-timeduration

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ITimeDurationFormatting](#type-itimedurationformatting)| false | _n/a_ |

## IActionAttachmentConfiguration :id=type-iactionattachmentconfiguration

No description available

Properties: [required](#type-iactionattachmentconfiguration-property-required), [allowMultipleAttachments](#type-iactionattachmentconfiguration-property-allowmultipleattachments)

### required :id=type-iactionattachmentconfiguration-property-required

This flag specifies if file attachments are required for this action. Defaults to `false`.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

### allowMultipleAttachments :id=type-iactionattachmentconfiguration-property-allowmultipleattachments

This flag specifies if multiple attachments are valid for this action. Note that the action will be executed once for every attachment.  For example, this flag could be set to `true` for the action `AttachDocument` in the `ExpenseSheets` container, as calling this action multiple times with new files will simply attach more files to the same expense sheet.  On the other hand, this flag should be `false` for the action `ImportDocument` in the table part of `DocumentArchives`, as running that action more than once will replace the document previously attached to the line.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

## IActionConfiguration :id=type-iactionconfiguration

No description available

Properties: [attachments](#type-iactionconfiguration-property-attachments), [parameters](#type-iactionconfiguration-property-parameters)

### attachments :id=type-iactionconfiguration-property-attachments

Specifies whether attachments (i.e. file uploads) should be available for this action.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IActionAttachmentConfiguration](#type-iactionattachmentconfiguration)| false | _n/a_ |

### parameters :id=type-iactionconfiguration-property-parameters

Specifies fields which act as parameters to this action. The values of these fields will be transmitted as singleton parameters when the action is executed.  Only fields from the card pane can be specified. The listed field names must be mapped to singleton identifiers in the card pane's `singletonIdentifiers` attribute.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[string\]| false | _n/a_ |

## IActionsRow :id=type-iactionsrow

Represents a row containing actions.

Properties: [actions](#type-iactionsrow-property-actions), [workspaceActions](#type-iactionsrow-property-workspaceactions), [title](#type-iactionsrow-property-title), [pane](#type-iactionsrow-property-pane)

### actions :id=type-iactionsrow-property-actions

The actions to be shown in this action row.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[*unknown*\]| false | _n/a_ |

### workspaceActions :id=type-iactionsrow-property-workspaceactions

Show workspace actions (such as edit, save, revert) in this actions row.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### title :id=type-iactionsrow-property-title

An optional, localizable title.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### pane :id=type-iactionsrow-property-pane

Optional pane which is used to resolve unqualified references in this scope. If nothing is specified then the pane from the parent scope is indirectly inherited.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IAmountFormatting :id=type-iamountformatting

No description available

## IAssignTrigger :id=type-iassigntrigger

A trigger that assigns a value to a field.

Properties: [assign](#type-iassigntrigger-property-assign)

### assign :id=type-iassigntrigger-property-assign

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Assign](#type-assign)| true | _n/a_ |

## IAuthenticationConfiguration :id=type-iauthenticationconfiguration

Set up authentication schemes.

Properties: [preferred](#type-iauthenticationconfiguration-property-preferred), [methods](#type-iauthenticationconfiguration-property-methods)

### preferred :id=type-iauthenticationconfiguration-property-preferred

The preferred method of performing login. This method determines the entry route when arriving from the bare, default '/' URL.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[AuthenticationType](#type-authenticationtype)| true | _n/a_ |

### methods :id=type-iauthenticationconfiguration-property-methods

Used to disable/enable individual login methods.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Methods](#type-methods)| true | _n/a_ |

## IAutoTimestampFormatting :id=type-iautotimestampformatting

No description available

## IAvailableFormats :id=type-iavailableformats

No description available

## IBindingSpecification :id=type-ibindingspecification

No description available

Properties: [binding](#type-ibindingspecification-property-binding), [container](#type-ibindingspecification-property-container)

### binding :id=type-ibindingspecification-property-binding

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| true | _n/a_ |

### container :id=type-ibindingspecification-property-container

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IContainerSpecification](#type-icontainerspecification)| true | _n/a_ |

## IBooleanFormatting :id=type-ibooleanformatting

No description available

## ICancelTransition :id=type-icanceltransition

No description available

Properties: [visible](#type-icanceltransition-property-visible), [title](#type-icanceltransition-property-title), [actions](#type-icanceltransition-property-actions)

### visible :id=type-icanceltransition-property-visible

Specifies if a dedicated cancel button should be shown. If `false`, then the wizard can still be cancelled by pressing Escape or clicking on the "x" icon in the corner of the wizard window.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### title :id=type-icanceltransition-property-title

The title of the dedicated cancel button. Defaults to "Cancel".

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### actions :id=type-icanceltransition-property-actions

A list of actions to perform upon activating this transition.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[*unknown*\]| false | _n/a_ |

## ICardPaneConfiguration :id=type-icardpaneconfiguration

No description available

Properties: [singletonIdentifiers](#type-icardpaneconfiguration-property-singletonidentifiers), [stateParameters](#type-icardpaneconfiguration-property-stateparameters), [navigationParameters](#type-icardpaneconfiguration-property-navigationparameters), [actions](#type-icardpaneconfiguration-property-actions), [cacheInitResponse](#type-icardpaneconfiguration-property-cacheinitresponse)

### singletonIdentifiers :id=type-icardpaneconfiguration-property-singletonidentifiers

Maps field names to singleton identifiers.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> string| false | _n/a_ |

### stateParameters :id=type-icardpaneconfiguration-property-stateparameters

Specifies _state parameter_ fields for this container.  State parameters are fields that are not persisted on the server side. In order for the state of these fields to be maintained across REST requests, their values have to be included in every request as singleton parameters.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[string\]| false | _n/a_ |

### navigationParameters :id=type-icardpaneconfiguration-property-navigationparameters

Specifies _navigation parameter_ fields for this container.  Navigation parameters are fields in the card part of a container that control the internal navigation state of the container. In particular, they control the resource which will be the target of actions performed on this container.  Fields defined as navigation parameters cannot be changed together with any other fields in the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[string\]| false | _n/a_ |

### actions :id=type-icardpaneconfiguration-property-actions

Additional configuration for actions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IActionConfiguration](#type-iactionconfiguration)| false | _n/a_ |

### cacheInitResponse :id=type-icardpaneconfiguration-property-cacheinitresponse

Specifies whether caching of _init_ responses is allowed for this pane.  If set to `true`, then _init_ responses will be cached; when set to `false`, they will not be cached. If not specified, the default behavior is to cache _init_ responses.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

## IContainerConfiguration :id=type-icontainerconfiguration

Specifies additional configuration options for a container.

Properties: [filter](#type-icontainerconfiguration-property-filter), [card](#type-icontainerconfiguration-property-card), [table](#type-icontainerconfiguration-property-table), [filterAsTable](#type-icontainerconfiguration-property-filterastable)

### filter :id=type-icontainerconfiguration-property-filter

Configuration for the filter pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IPaneConfiguration](#type-ipaneconfiguration)| false | _n/a_ |

### card :id=type-icontainerconfiguration-property-card

Configuration for the card pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ICardPaneConfiguration](#type-icardpaneconfiguration)| false | _n/a_ |

### table :id=type-icontainerconfiguration-property-table

Configuration for the table pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ITablePaneConfiguration](#type-itablepaneconfiguration)| false | _n/a_ |

### filterAsTable :id=type-icontainerconfiguration-property-filterastable

Configuration for the filter-as-table pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IFilterAsTablePaneConfiguration](#type-ifilterastablepaneconfiguration)| false | _n/a_ |

## IContainerSpecification :id=type-icontainerspecification

No description available

Properties: [source](#type-icontainerspecification-property-source), [type](#type-icontainerspecification-property-type), [name](#type-icontainerspecification-property-name), [parameters](#type-icontainerspecification-property-parameters), [restriction](#type-icontainerspecification-property-restriction), [bindings](#type-icontainerspecification-property-bindings), [triggers](#type-icontainerspecification-property-triggers), [orderBy](#type-icontainerspecification-property-orderby), [sharedRecord](#type-icontainerspecification-property-sharedrecord)

### source :id=type-icontainerspecification-property-source

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### type :id=type-icontainerspecification-property-type

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IPaneType](#type-ipanetype)| true | _n/a_ |

### name :id=type-icontainerspecification-property-name

String alias for pane names.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### parameters :id=type-icontainerspecification-property-parameters

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> *unknown*| false | _n/a_ |

### restriction :id=type-icontainerspecification-property-restriction

String alias for an expression.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### bindings :id=type-icontainerspecification-property-bindings

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[[IBindingSpecification](#type-ibindingspecification)\]| false | _n/a_ |

### triggers :id=type-icontainerspecification-property-triggers

Defines triggers that will be executed at specific pane events.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ITriggers](#type-itriggers)| false | _n/a_ |

### orderBy :id=type-icontainerspecification-property-orderby

Defines the default sorting order for this pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[[IOrderBy](#type-iorderby)\]| false | _n/a_ |

### sharedRecord :id=type-icontainerspecification-property-sharedrecord

Enables record sharing for this pane.  When this property is set to some string (the sharing key), then the record selected in this pane will be shared with other panes that use the same key. If you switch between workspaces where panes use the same sharing key, the same record as was selected in one workspace will be automatically selected in others.  Note that this property only takes effect for panes of type "search-filter". All panes using the same sharing key must be defined on the same container - it is not allowed to share records between panes using different containers.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IDataBindings :id=type-idatabindings

No description available

Properties: [container](#type-idatabindings-property-container)

### container :id=type-idatabindings-property-container

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IContainerSpecification](#type-icontainerspecification)| true | _n/a_ |

## IDateFormatting :id=type-idateformatting

No description available

## IEnumFormatting :id=type-ienumformatting

No description available

## IFilterAsTablePaneConfiguration :id=type-ifilterastablepaneconfiguration

No description available

Properties: [fields](#type-ifilterastablepaneconfiguration-property-fields), [actions](#type-ifilterastablepaneconfiguration-property-actions)

### fields :id=type-ifilterastablepaneconfiguration-property-fields

Configuration of additional fields for the filter-as-table pane.  By default, filter-as-table includes only fields that have the same name and type in the filter pane as in the card pane. However, additional fields can be configured:  1) If a field from the filter pane exists has a corresponding field in the card pane,     but with a different name, then a mapping between the names can be defined. 2) If a field is available in the filter pane only, then such a field can be shown as a read-only field     in the filter-as-table pane.  This property maps field names from the filter pane (which are also the names used in the filter-as-table pane) to a configuration of each field.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> *unknown*| false | _n/a_ |

### actions :id=type-ifilterastablepaneconfiguration-property-actions

Additional configuration for actions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IActionConfiguration](#type-iactionconfiguration)| false | _n/a_ |

## IFormats :id=type-iformats

No description available

Properties: [preferred](#type-iformats-property-preferred), [fixed](#type-iformats-property-fixed), [available](#type-iformats-property-available)

### preferred :id=type-iformats-property-preferred

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### fixed :id=type-iformats-property-fixed

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### available :id=type-iformats-property-available

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IAvailableFormats](#type-iavailableformats)| true | _n/a_ |

## IGLobalDefinitions :id=type-iglobaldefinitions

Definitions are used to share common referable concepts and items across different workspaces and areas of iAccess.

Properties: [css](#type-iglobaldefinitions-property-css), [infoBubbles](#type-iglobaldefinitions-property-infobubbles), [sizes](#type-iglobaldefinitions-property-sizes), [styles](#type-iglobaldefinitions-property-styles), [colors](#type-iglobaldefinitions-property-colors)

### css :id=type-iglobaldefinitions-property-css

Predefined CSS that can be referred and used across all workspaces.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> *unknown*| true | _n/a_ |

### infoBubbles :id=type-iglobaldefinitions-property-infobubbles

Info-bubbles that can be used across all workspaces.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IReusableInfoBubbleDefinition](#type-ireusableinfobubbledefinition)| true | _n/a_ |

### sizes :id=type-iglobaldefinitions-property-sizes

Mapping between symbolic names to pixel width.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Sizes](#type-sizes)| true | _n/a_ |

### styles :id=type-iglobaldefinitions-property-styles

Reusable style definitions that can be applied across all workspaces.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> *unknown*| true | _n/a_ |

### colors :id=type-iglobaldefinitions-property-colors

Reusable colors used across different workspaces

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> string| true | _n/a_ |

## IHeading :id=type-iheading

Configuration of the header area of a workspace. The header is used to communicate the title of the workspace, provide access to the primary navigation facility, and optionally allow the user to create instances of the workspace's main data type.

Properties: [navigation](#type-iheading-property-navigation), [createAction](#type-iheading-property-createaction), [title](#type-iheading-property-title), [pane](#type-iheading-property-pane)

### navigation :id=type-iheading-property-navigation

Optional navigation facility to navigate between different instances of the main data entity in this workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### createAction :id=type-iheading-property-createaction

If specified, a creation action will be added to the workspace for adding a new record.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IHeadingCreateAction](#type-iheadingcreateaction)| false | _n/a_ |

### title :id=type-iheading-property-title

An optional, localizable title.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### pane :id=type-iheading-property-pane

Optional pane which is used to resolve unqualified references in this scope. If nothing is specified then the pane from the parent scope is indirectly inherited.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IHeadingCreateAction :id=type-iheadingcreateaction

No description available

Properties: [pane](#type-iheadingcreateaction-property-pane), [wizardWorkspace](#type-iheadingcreateaction-property-wizardworkspace), [title](#type-iheadingcreateaction-property-title)

### pane :id=type-iheadingcreateaction-property-pane

The pane where the create action will be executed.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### wizardWorkspace :id=type-iheadingcreateaction-property-wizardworkspace

A wizard that will be shown when this action is clicked.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IWizardWorkspace](#type-iwizardworkspace)| false | _n/a_ |

### title :id=type-iheadingcreateaction-property-title

An optional, localizable title.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IIntegerFormatting :id=type-iintegerformatting

No description available

Properties: [zeroSuppression](#type-iintegerformatting-property-zerosuppression)

### zeroSuppression :id=type-iintegerformatting-property-zerosuppression

True if zero values should be suppressed.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

## ILanguageConfiguration :id=type-ilanguageconfiguration

No description available

Properties: [preferred](#type-ilanguageconfiguration-property-preferred), [fixed](#type-ilanguageconfiguration-property-fixed)

### preferred :id=type-ilanguageconfiguration-property-preferred

The preferred locale, e.g., 'da_DK'

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### fixed :id=type-ilanguageconfiguration-property-fixed

True if the language is fixed and cannot be changed by the end-user. This removes the language selector from the both login screen and settings dialog.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

## ILocalDefinitions :id=type-ilocaldefinitions

Definitions that are used to share common referable items within a single workspace.

Properties: [infoBubbles](#type-ilocaldefinitions-property-infobubbles)

### infoBubbles :id=type-ilocaldefinitions-property-infobubbles

Info-bubbles that can be used multiple times across the same workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IReusableInfoBubbleDefinition](#type-ireusableinfobubbledefinition)| false | _n/a_ |

## IMenu :id=type-imenu

The menu provides access to the workspaces that are available to the logged-in user. A menu consists of workspaces ordered in groups. Different users may see different sets of menu groups and items depending on the user's privileges and context.

Properties: [restoreLastWorkspace](#type-imenu-property-restorelastworkspace), [groups](#type-imenu-property-groups)

### restoreLastWorkspace :id=type-imenu-property-restorelastworkspace

Restore the last used workspace on login. Default is true.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### groups :id=type-imenu-property-groups

The set of menu groups available in the menu.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[[IMenuGroup](#type-imenugroup)\]| true | _n/a_ |

## IMenuGroup :id=type-imenugroup

A group of workspaces arranged under a common title

Properties: [title](#type-imenugroup-property-title), [items](#type-imenugroup-property-items), [visible](#type-imenugroup-property-visible)

### title :id=type-imenugroup-property-title

The title of a group of workspaces in the menu.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### items :id=type-imenugroup-property-items

The workspaces or links contained in this menu group.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[*unknown*\]| false | _n/a_ |

### visible :id=type-imenugroup-property-visible

Optional condition that determines if a menu part (group or item) should be visible or not.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## INotificationConfiguration :id=type-inotificationconfiguration

Represents the configuration of notification reload and recalculation intervals.

Properties: [recalculation](#type-inotificationconfiguration-property-recalculation), [types](#type-inotificationconfiguration-property-types)

### recalculation :id=type-inotificationconfiguration-property-recalculation

The recalculation settings determine when the first recalculation of the end-user's notifications occur and what the interval between subsequent recalculations is. All values are specified in minutes.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Recalculation](#type-recalculation)| true | _n/a_ |

### types :id=type-inotificationconfiguration-property-types

Supported notification types as specified in the MNSL files.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [INotificationType](#type-inotificationtype)| true | _n/a_ |

## INotificationType :id=type-inotificationtype

No description available

Properties: [workspace](#type-inotificationtype-property-workspace), [parameters](#type-inotificationtype-property-parameters)

### workspace :id=type-inotificationtype-property-workspace

The name of the workspace

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### parameters :id=type-inotificationtype-property-parameters

A map of url parameters for the workspace linking to the Focus key in question.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> string| false | _n/a_ |

## IOrderBy :id=type-iorderby

A field used for sorting records in a pane.

Properties: [source](#type-iorderby-property-source), [order](#type-iorderby-property-order)

### source :id=type-iorderby-property-source

String alias for field source/model names.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### order :id=type-iorderby-property-order

The sorting order for this field.  If not specified, then the default order is `ascending`.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IPageLayouts :id=type-ipagelayouts

No description available

## IPaneConfiguration :id=type-ipaneconfiguration

No description available

Properties: [actions](#type-ipaneconfiguration-property-actions)

### actions :id=type-ipaneconfiguration-property-actions

Additional configuration for actions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IActionConfiguration](#type-iactionconfiguration)| false | _n/a_ |

## IPaneType :id=type-ipanetype

No description available

## IPlatformConfiguration :id=type-iplatformconfiguration

No description available

Properties: [usageTracking](#type-iplatformconfiguration-property-usagetracking), [containers](#type-iplatformconfiguration-property-containers), [typeAhead](#type-iplatformconfiguration-property-typeahead)

### usageTracking :id=type-iplatformconfiguration-property-usagetracking

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IUsageTrackingConfiguration](#type-iusagetrackingconfiguration)| true | _n/a_ |

### containers :id=type-iplatformconfiguration-property-containers

Additional configuration for containers on a Maconomy installation.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IContainerConfiguration](#type-icontainerconfiguration)| true | _n/a_ |

### typeAhead :id=type-iplatformconfiguration-property-typeahead

Configuration of the type-ahead functionality.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ITypeAheadConfiguration](#type-itypeaheadconfiguration)| false | _n/a_ |

## IRealFormatting :id=type-irealformatting

No description available

Properties: [zeroSuppression](#type-irealformatting-property-zerosuppression)

### zeroSuppression :id=type-irealformatting-property-zerosuppression

True if zero values should be suppressed.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

## IRecordHeading :id=type-irecordheading

No description available

Properties: [title](#type-irecordheading-property-title), [subTitle](#type-irecordheading-property-subtitle), [status](#type-irecordheading-property-status), [pane](#type-irecordheading-property-pane)

### title :id=type-irecordheading-property-title

An optional title for the sub heading of the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### subTitle :id=type-irecordheading-property-subtitle

An optional sub-title for the sub heading of the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### status :id=type-irecordheading-property-status

An optional status element for the sub heading of the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IStatusElement](#type-istatuselement)| false | _n/a_ |

### pane :id=type-irecordheading-property-pane

Optional pane which is used to resolve unqualified references in this scope. If nothing is specified then the pane from the parent scope is indirectly inherited.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IReusableInfoBubbleDefinition :id=type-ireusableinfobubbledefinition

A definition of a reusable info bubble.

Properties: [parameters](#type-ireusableinfobubbledefinition-property-parameters), [width](#type-ireusableinfobubbledefinition-property-width), [position](#type-ireusableinfobubbledefinition-property-position), [title](#type-ireusableinfobubbledefinition-property-title), [subTitle](#type-ireusableinfobubbledefinition-property-subtitle), [rows](#type-ireusableinfobubbledefinition-property-rows), [pane](#type-ireusableinfobubbledefinition-property-pane)

### parameters :id=type-ireusableinfobubbledefinition-property-parameters

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IReusableInfoBubbleParameters](#type-ireusableinfobubbleparameters)| true | _n/a_ |

### width :id=type-ireusableinfobubbledefinition-property-width

You can optionally specify the width of the Info-bubble:  xs: 200 px sm: 300 px md: 400 px lg: 400 px xl: 400 px  The default behavior is:  1 column is rendered xs 2 columns is rendered sm >2 columns is rendered md

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### position :id=type-ireusableinfobubbledefinition-property-position

An optional position of the info bubble. Right is default.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### title :id=type-ireusableinfobubbledefinition-property-title

The title or heading of the info bubble

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### subTitle :id=type-ireusableinfobubbledefinition-property-subtitle

The sub heading of the info bubble

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### rows :id=type-ireusableinfobubbledefinition-property-rows

The rows or content of the info bubble

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[*unknown*\]| true | _n/a_ |

### pane :id=type-ireusableinfobubbledefinition-property-pane

Optional pane which is used to resolve unqualified references in this scope. If nothing is specified then the pane from the parent scope is indirectly inherited.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IReusableInfoBubbleParameters :id=type-ireusableinfobubbleparameters

Defines the parameters for the reusable info bubble.

Properties: [fields](#type-ireusableinfobubbleparameters-property-fields), [foreignKeys](#type-ireusableinfobubbleparameters-property-foreignkeys)

### fields :id=type-ireusableinfobubbleparameters-property-fields

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[string\]| true | _n/a_ |

### foreignKeys :id=type-ireusableinfobubbleparameters-property-foreignkeys

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[string\]| false | _n/a_ |

## ISettings :id=type-isettings

Settings represents formats, language, and other end-user configurable properties.

Properties: [language](#type-isettings-property-language), [formats](#type-isettings-property-formats), [minutesThreshold](#type-isettings-property-minutesthreshold), [menuSearch](#type-isettings-property-menusearch), [formatting](#type-isettings-property-formatting)

### language :id=type-isettings-property-language

The language configuration determines default language and whether the end-user can change language.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ILanguageConfiguration](#type-ilanguageconfiguration)| true | _n/a_ |

### formats :id=type-isettings-property-formats

The formats configuration determines the data formatting as well as whether this can be changed by the end-user.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IFormats](#type-iformats)| true | _n/a_ |

### minutesThreshold :id=type-isettings-property-minutesthreshold

The minute threshold determines when a time entry is interpreted as minutes or as hours. Default is '10' which means that an entry of '10' will be interpreted as 10 minutes, and an entry of '11' will be interpreted as 11 hours.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| false | _n/a_ |

### menuSearch :id=type-isettings-property-menusearch

The menuSearch configuration determines if the search component is enabled in the menu

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

### formatting :id=type-isettings-property-formatting

Configure formatting rules for data types.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Formatting](#type-formatting)| true | _n/a_ |

## IShellConfiguration :id=type-ishellconfiguration

The application shell covers the menu, documentation, notifications and auxiliary features such as settings, change password and about information.

Properties: [menu](#type-ishellconfiguration-property-menu), [documentationUrl](#type-ishellconfiguration-property-documentationurl), [settings](#type-ishellconfiguration-property-settings), [notifications](#type-ishellconfiguration-property-notifications)

### menu :id=type-ishellconfiguration-property-menu

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IMenu](#type-imenu)| true | _n/a_ |

### documentationUrl :id=type-ishellconfiguration-property-documentationurl

The URL used for hosted help. Can be a simple string with variables such as <version>.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### settings :id=type-ishellconfiguration-property-settings

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ISettings](#type-isettings)| true | _n/a_ |

### notifications :id=type-ishellconfiguration-property-notifications

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[INotificationConfiguration](#type-inotificationconfiguration)| true | _n/a_ |

## IStatusElement :id=type-istatuselement

Status elements are used in forms for rendering status information about a record.

Properties: [css](#type-istatuselement-property-css), [class](#type-istatuselement-property-class), [appearance](#type-istatuselement-property-appearance), [rendering](#type-istatuselement-property-rendering), [open](#type-istatuselement-property-open), [mandatory](#type-istatuselement-property-mandatory), [autoSubmit](#type-istatuselement-property-autosubmit), [visible](#type-istatuselement-property-visible), [title](#type-istatuselement-property-title), [titleValue](#type-istatuselement-property-titlevalue), [titleSource](#type-istatuselement-property-titlesource), [source](#type-istatuselement-property-source), [mask](#type-istatuselement-property-mask)

### css :id=type-istatuselement-property-css

Maps from CSS property keys to their values (strings)

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> string| false | _n/a_ |

### class :id=type-istatuselement-property-class

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### appearance :id=type-istatuselement-property-appearance

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### rendering :id=type-istatuselement-property-rendering

Represents the two different ways of rendering a layout (or part of a layout).

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### open :id=type-istatuselement-property-open

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### mandatory :id=type-istatuselement-property-mandatory

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### autoSubmit :id=type-istatuselement-property-autosubmit

Specifies that changes to this field should be automatically saved.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### visible :id=type-istatuselement-property-visible

A condition specifying when this element should be visible. If not specified, the tab is visible.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### title :id=type-istatuselement-property-title

An optional, localized text to show.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### titleValue :id=type-istatuselement-property-titlevalue

An optional, text coming from value of a field.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### titleSource :id=type-istatuselement-property-titlesource

An optional, text coming from the title of another field.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### source :id=type-istatuselement-property-source

The underlying pane field that provides data for this status block.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### mask :id=type-istatuselement-property-mask

A mask map a given internal status value to a title and css. In time sheets, you can for instance map the status character '1' to the title 'Due' and the color red.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IStatusIndication](#type-istatusindication)| true | _n/a_ |

## IStatusIndication :id=type-istatusindication

No description available

Properties: [title](#type-istatusindication-property-title), [css](#type-istatusindication-property-css), [info](#type-istatusindication-property-info)

### title :id=type-istatusindication-property-title

String alias for localizable, end-user visible, static titles.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### css :id=type-istatusindication-property-css

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### info :id=type-istatusindication-property-info

A definition of an inline info-bubble or a reference to a reusable info-bubble.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

## IStringFormatting :id=type-istringformatting

No description available

## ITablePaneConfiguration :id=type-itablepaneconfiguration

No description available

Properties: [actions](#type-itablepaneconfiguration-property-actions), [cacheInitResponse](#type-itablepaneconfiguration-property-cacheinitresponse)

### actions :id=type-itablepaneconfiguration-property-actions

Additional configuration for actions.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IActionConfiguration](#type-iactionconfiguration)| false | _n/a_ |

### cacheInitResponse :id=type-itablepaneconfiguration-property-cacheinitresponse

Specifies whether caching of _init_ responses is allowed for this pane.  If set to `true`, then _init_ responses will be cached; when set to `false`, they will not be cached. If not specified, the default behavior is to cache _init_ responses.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

## ITimeDurationFormatting :id=type-itimedurationformatting

No description available

Properties: [type](#type-itimedurationformatting-property-type), [zeroSuppression](#type-itimedurationformatting-property-zerosuppression)

### type :id=type-itimedurationformatting-property-type

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### zeroSuppression :id=type-itimedurationformatting-property-zerosuppression

True if zero values should be suppressed.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

## ITimeFormatting :id=type-itimeformatting

No description available

## ITriggers :id=type-itriggers

Defines triggers that will be executed at specific pane events.

Properties: [init](#type-itriggers-property-init)

### init :id=type-itriggers-property-init

Specifies triggers to be executed when a new record is created in a pane.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[[IAssignTrigger](#type-iassigntrigger)\]| false | _n/a_ |

## ITypeAheadConfiguration :id=type-itypeaheadconfiguration

No description available

Properties: [enabled](#type-itypeaheadconfiguration-property-enabled), [maximumQueueLength](#type-itypeaheadconfiguration-property-maximumqueuelength)

### enabled :id=type-itypeaheadconfiguration-property-enabled

This flag enables type-ahead for all workspaces.  Default: `true`

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### maximumQueueLength :id=type-itypeaheadconfiguration-property-maximumqueuelength

The maximum number of operations that can be scheduled for execution.  Default: `5`

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| false | _n/a_ |

## IUsageTrackingConfiguration :id=type-iusagetrackingconfiguration

No description available

Properties: [enabled](#type-iusagetrackingconfiguration-property-enabled), [endUserOptIn](#type-iusagetrackingconfiguration-property-enduseroptin), [trackingId](#type-iusagetrackingconfiguration-property-trackingid)

### enabled :id=type-iusagetrackingconfiguration-property-enabled

This flag enables usage tracking for the entire iAccess installation. Default: True

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

### endUserOptIn :id=type-iusagetrackingconfiguration-property-enduseroptin

This flag enables end-user opt-in notification about usage tracking.  When the end-user opts-in, the notification is not shown for a year unless cookies are cleared. Default: True

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

### trackingId :id=type-iusagetrackingconfiguration-property-trackingid

Google Analytics tracker ID can be provided here for custom tracking of iAccess usage.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

## IWizardWorkflow :id=type-iwizardworkflow

No description available

## IWizardWorkspace :id=type-iwizardworkspace

Configuration of an individual wizard workspace.  A wizard workspace is similar to a regular workspace in that it has a name, a title and it exposes data though panes set up in the data-bindings part. However, as opposed to a regular workspace, this workspace leads the user through a number of steps (set up in the workflow part) and can display a different layout for each step (these are configured in the page-layouts part).

Properties: [name](#type-iwizardworkspace-property-name), [title](#type-iwizardworkspace-property-title), [size](#type-iwizardworkspace-property-size), [definitions](#type-iwizardworkspace-property-definitions), [variables](#type-iwizardworkspace-property-variables), [dataBindings](#type-iwizardworkspace-property-databindings), [workflow](#type-iwizardworkspace-property-workflow), [pageLayouts](#type-iwizardworkspace-property-pagelayouts), [sideEffects](#type-iwizardworkspace-property-sideeffects), [cancel](#type-iwizardworkspace-property-cancel)

### name :id=type-iwizardworkspace-property-name

The internal, unique, non-localizable name of the wizard workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### title :id=type-iwizardworkspace-property-title

The title of the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### size :id=type-iwizardworkspace-property-size

The size of the wizard window. If not specified the medium size will be applied.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### definitions :id=type-iwizardworkspace-property-definitions

Definitions of items that can be reused many times within this workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ILocalDefinitions](#type-ilocaldefinitions)| false | _n/a_ |

### variables :id=type-iwizardworkspace-property-variables

Definition of client-side variables.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IWorkspaceVariables](#type-iworkspacevariables)| false | _n/a_ |

### dataBindings :id=type-iwizardworkspace-property-databindings

Configuration of the panes that compose this workspace and how these panes are bound together.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[[IBindingSpecification](#type-ibindingspecification)\]| false | _n/a_ |

### workflow :id=type-iwizardworkspace-property-workflow

Configuration of the states in the wizard.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IWizardWorkflow](#type-iwizardworkflow)| true | _n/a_ |

### pageLayouts :id=type-iwizardworkspace-property-pagelayouts

Definition of the layouts for the pages in the wizard.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IPageLayouts](#type-ipagelayouts)| true | _n/a_ |

### sideEffects :id=type-iwizardworkspace-property-sideeffects

Specifies if the wizard makes changes that affect the host workspace.  If not specified, then a wizard is assumed to have side effects (i.e. the default value is `true`).  This field can be set to `false` if a wizard is known to _not_ make any changes to the data which is shown in the host workspace. Setting this field to `false` has the following consequences: - the host workspace will not be refreshed when the wizard is closed, - the wizard can be invoked even if the host workspace has unsaved changes.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| false | _n/a_ |

### cancel :id=type-iwizardworkspace-property-cancel

Specifies the behavior for cancelling the wizard. This setting provides a default value that can be overriden in each workflow state.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ICancelTransition](#type-icanceltransition)| false | _n/a_ |

## IWorkspace :id=type-iworkspace

Configuration of an individual workspace. A workspace is defined by a unique name and a recognizable title. The data exposed by the workspace is set up in the data-bindings part, and the appearance of that data is defined by its layout.

Properties: [name](#type-iworkspace-property-name), [state](#type-iworkspace-property-state), [title](#type-iworkspace-property-title), [definitions](#type-iworkspace-property-definitions), [dataBindings](#type-iworkspace-property-databindings), [layout](#type-iworkspace-property-layout)

### name :id=type-iworkspace-property-name

The internal, unique, non-localizable name of the workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### state :id=type-iworkspace-property-state

Optional marker to indicate if the workspace is in beta or test.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### title :id=type-iworkspace-property-title

The title of the workspace. Can be overridden by the menu configuration.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| true | _n/a_ |

### definitions :id=type-iworkspace-property-definitions

Definitions of items that can be reused many times within this workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[ILocalDefinitions](#type-ilocaldefinitions)| false | _n/a_ |

### dataBindings :id=type-iworkspace-property-databindings

Configuration of the panes that compose this workspace and how these panes are bound together.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IDataBindings](#type-idatabindings)| true | _n/a_ |

### layout :id=type-iworkspace-property-layout

Configuration of the layout of data and actions associated with this workspace.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IWorkspaceLayout](#type-iworkspacelayout)| true | _n/a_ |

## IWorkspaceConfiguration :id=type-iworkspaceconfiguration

Representation of both general configuration spanning all workspaces as well as the setup of data bindings and layout for individual workspaces. A workspace will, however, not appear in iAccess until it is referred from the menu.

Properties: [workspaces](#type-iworkspaceconfiguration-property-workspaces), [definitions](#type-iworkspaceconfiguration-property-definitions)

### workspaces :id=type-iworkspaceconfiguration-property-workspaces

The collection of all workspaces available to iAccess. Each workspace can be retrieved by lookup using an internal, non-localizable name (@link WorkspaceName}.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> [IWorkspace](#type-iworkspace)| true | _n/a_ |

### definitions :id=type-iworkspaceconfiguration-property-definitions

Global definitions contain pre-defined colors and other referrable items that span all workspaces. These definitions are used both for convenience and as a way of ensuring a uniform look and feel across all workspaces.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IGLobalDefinitions](#type-iglobaldefinitions)| true | _n/a_ |

## IWorkspaceLayout :id=type-iworkspacelayout

Represents the layout for the entire workspace area.

Properties: [heading](#type-iworkspacelayout-property-heading), [rendering](#type-iworkspacelayout-property-rendering), [list](#type-iworkspacelayout-property-list), [record](#type-iworkspacelayout-property-record), [rows](#type-iworkspacelayout-property-rows), [actionBar](#type-iworkspacelayout-property-actionbar)

### heading :id=type-iworkspacelayout-property-heading

The heading area should communicate the overall purpose of this workspace and facilitate navigation between instances of the main data entity. Often a create action will also be available for the main data entity.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IHeading](#type-iheading)| true | _n/a_ |

### rendering :id=type-iworkspacelayout-property-rendering

The default rendering of a workspace is 'presentation'. If a rendering is specified for the entire layout using this property then the rendering will be fixed to that mode. This is primarily used to force a layout to always be render in editable mode.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string| false | _n/a_ |

### list :id=type-iworkspacelayout-property-list

Controls whether the workspace should show a "list view", and optionally defines a layout for the list view.  This property can contain one of the three possible values: 1. A list view layout. 2. The value `true` indicating that a list view layout should be autogenerated. 3. The value `false` indicating that no list view should be shown in this workspace.  If this property is not specified, then it defaults to `true`.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|*unknown*| false | _n/a_ |

### record :id=type-iworkspacelayout-property-record

The record heading area should communicate the overall data entity of the workspace. This should contain the primary identifier of the currently shown data entity.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IRecordHeading](#type-irecordheading)| false | _n/a_ |

### rows :id=type-iworkspacelayout-property-rows

The main body of a workspace layout consists of an array of layout rows.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|array \[*unknown*\]| true | _n/a_ |

### actionBar :id=type-iworkspacelayout-property-actionbar

The actions to be shown in this action row.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[IActionsRow](#type-iactionsrow)| false | _n/a_ |

## IWorkspaceVariables :id=type-iworkspacevariables

No description available

## Maconomy :id=type-maconomy

No description available

Properties: [enabled](#type-maconomy-property-enabled)

### enabled :id=type-maconomy-property-enabled

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

## Methods :id=type-methods

Used to disable/enable individual login methods.

Properties: [maconomy](#type-methods-property-maconomy), [domain](#type-methods-property-domain), [sso](#type-methods-property-sso), [azure](#type-methods-property-azure)

### maconomy :id=type-methods-property-maconomy

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Maconomy](#type-maconomy)| false | _n/a_ |

### domain :id=type-methods-property-domain

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Domain](#type-domain)| false | _n/a_ |

### sso :id=type-methods-property-sso

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Sso](#type-sso)| false | _n/a_ |

### azure :id=type-methods-property-azure

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|[Azure](#type-azure)| false | _n/a_ |

## Recalculation :id=type-recalculation

The recalculation settings determine when the first recalculation of the end-user's notifications occur and what the interval between subsequent recalculations is. All values are specified in minutes.

Properties: [initialDelay](#type-recalculation-property-initialdelay), [interval](#type-recalculation-property-interval), [quarantinePeriod](#type-recalculation-property-quarantineperiod)

### initialDelay :id=type-recalculation-property-initialdelay

The initial delay in minutes between the time the user logs in and when the first recalculation of notifications is requested. The reason for not requesting recalculation immediately is that the server should be set up to recalculate every night such that the notifications are already up to date on login.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### interval :id=type-recalculation-property-interval

The interval in minutes between each request for recalculation of the user's notifications. Care should be taken when setting this interval as recalculation of notifications can be a very performance intensive process. If the interval is set to a low value then overall system performance may degrade significantly.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### quarantinePeriod :id=type-recalculation-property-quarantineperiod

The quarantine period property defines the minimum quarantine period between repeated client requests for recalculation of notifications.

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

## Sizes :id=type-sizes

Mapping between symbolic names to pixel width.

Properties: [xs](#type-sizes-property-xs), [sm](#type-sizes-property-sm), [md](#type-sizes-property-md), [lg](#type-sizes-property-lg), [xl](#type-sizes-property-xl), [custom](#type-sizes-property-custom)

### xs :id=type-sizes-property-xs

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### sm :id=type-sizes-property-sm

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### md :id=type-sizes-property-md

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### lg :id=type-sizes-property-lg

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### xl :id=type-sizes-property-xl

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|number| true | _n/a_ |

### custom :id=type-sizes-property-custom

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|string -> number| true | _n/a_ |

## Sso :id=type-sso

No description available

Properties: [enabled](#type-sso-property-enabled)

### enabled :id=type-sso-property-enabled

No description available

| Type | Required             | Default Value |
|------|----------------------|---------------|
|boolean| true | _n/a_ |

