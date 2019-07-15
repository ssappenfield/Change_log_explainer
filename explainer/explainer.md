# Version History Explainer

## Introduction 

New versions of apps have new features, bug fixes & more. With PWAs' everchanging nature, it's hard to surface this sort of information in places like app stores. Version history offers a mechanism for developers to point to a web-based changelog for their app to highlight this information.

## Why is a PWA Version History Needed?

There is currently no standard way for PWA's changelog to be displayed or accessed.

## Goals for v1

- Enable developers to display their PWA's changelog in a standardized fashion
- Enable user to access PWAs change log easily within the app 

## Use Cases

Most PWAs are regularly updated, and by providing end users access to information concerning these updates, the users understanding of the app would improve.  Also, app accessibility for end users would increase as a result of the following:

- Alert end users of a change 
- Reengagement of end-users to the application 
- Enable end users to discover what has changed in the application 
- Application support scenarios
	
A User Agent might choose to expose a version history as follows:

![Uber PWA](imgs/start.png)

![Clicking the … menu](imgs/start_select.png)

![… menu contents](imgs/dropdown.png)

![Selecting App Info](imgs/drop_down_select.png)

![App Info popup](imgs/App_info_pop_up.png)

![Selecting Version History from App Info](imgs/popup_select.png)

![Displaying version history from Uber PWA](imgs/version_history.png)

## Version History Proposal

The solution proposed in this explainer is the addition of a new members to the Web App Manifest: version.

```idl
dictionary WebAppManifest {
  …
  dictionary version;
}
```

This member would be defined as included as below:

```idl
dictionary version {
  USVString current;
  Required sequence<Resource> history;
}

dictionary Resource{
  USVString url;
  USVString type;
}
```

### Version Definition

#### `history`

The path to one or more Resources.
	
#### `current`

Optional. A human-readable label for current version name.

### Resource Definition

#### `url`

The url to load when users select "Version history". This URL must exist within the navigation scope (scope) defined in the manifest. If the manifest-url is a relative URL, the base URL will be the URL of the manifest. Example urls: [Twitter Release Notes](https://twitter.com/i/release_notes), [rubygem CHANGELOG file](https://github.com/botanicus/changelog/blob/master/CHANGELOG).

#### `type`

Provides the MIME type of file found at `url` 

### Example

```json
version: {
  current: "1.0.1"
  history: [{
    url: "https://foo.com/history",
    type: "text/html"
  }]
}
```

## Existing Solutions

**iOS App Store** displays version name, release date, and brief description of changes made for each version:

![Uber app in the iOS App Store](imgs/iosappstore.jpg)

**Microsoft store** displays an overview of changes that came with the latest version:

![Slack in the Microsoft Store](imgs/microsoft-store.png)

[GitHub releases](https://developer.github.com/v3/repos/releases/): can display to users important releases on GitHub developers


## Open Questions

1. Should history be stored as a dictionary instead of a collection?
2. Alternative formats for storing version data?
3. Are there titles other than "Version History" that would be preferable?
