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

	
A user agent might choose to expose a version history as follows:

![start page](imgs/start.png)


## Version History Proposal

 The solution proposed in this explainer is the addition of a new members to the Web App Manifest: version.
```	
	dictionary WebAppManifest {
		…
		dictionary version;
	}
```
This member would be defined as included as below:
```
	dictionary version {
		USVString current;
		Required sequence<Resource> history;
	}

	dictionary Resource{
		USVString url;
		USVString type;
	}
```
**history**<br/>
	The path to one or more Resources
	
**url**<br/>
	The url that loads when users select "Version history". This URL must exist within the navigation scope (scope) defined in the manifest. If the manifest-url is a relative URL, the base URL will be the URL of the manifest. Example urls: [twitter](https://twitter.com/i/release_notes), [rubygems](https://rubygems.org/gems/changelog/versions/0.8)

**type** <br/>
	Provides type of file found at url 

**Current**<br/>
	Optional. A human-readable label for current version name

**Example**:<br/>
```
	version: {
	  current: "1.0.1"
	  history: [{
	    url: "https://foo.com/history",
	    type: "text/html"
	  }]
	}
```
## Existing Solutions
**IOS App Store Version History**: displays version name, release date, and brief description of changes made for each version<br/>
![ios app store](imgs/iosappstore.jpg)<br/>
**Slack App at Microsoft store**: displays an overview of changes that came with the latest version<br/>
![microsoft changlog](imgs/microsoft-store.png)<br/>

GitHub releases: can display to users important releases on GitHub developers
https://developer.github.com/v3/repos/releases/ 
## Open Question
1. Should history be stored as a dictionary instead of a collection?
2. Alternative formats for storing version data?
3. Are there titles other than "Version History" that would be preferable?
