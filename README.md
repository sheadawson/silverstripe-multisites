# SilverStripe Multisites

## Overview

Allows for multiple websites to be managed through a single site tree. 

This is an alternative module to the Subsites module; it avoids any session
tracking of the 'current' website, and doesn't perform any query modification 
at runtime to change the 'site' context of queries you execute

## Installation

* Add the module and the multivaluefield module
* Run `dev/build`

## Setting up sites (and additional sites)

* In the CMS go to the Pages section and click on the Website 
* Enter in the full path to the site in the 'Host' field, without the `http://` 
  lead - eg `mysitedomain.com` or `localhost/sub/folder` for a development site
* Hit save
* To add a new site, click the Pages section; you should have an 'Add site' 
  button
* Enter details about the new site, the Host field being the most important

## Assets management

You can optionally manage each site's assets in it's own subfolder of the root assets/ directory. Add the following extensions in your mysite/config.yml file and run ?flush=1. When editing a Site in the CMS, you now have the option to select a subfolder of assets/ to contain all assets for that site. This folder will be automatically created upon a) saving the site or b) visiting a page in the cms that has an upload field.

```
FileField:
  extensions:
    - MultisitesFileFieldExtension

HtmlEditorField_Toolbar:
  extensions:
    - MultisitesHtmlEditorField_ToolbarExtension
```

Files uploaded through the HTMLEditor will now be uploaded into assets/yoursite/Uploads. If you have custom upload fields in the cms however, you will need to add the following configuration to them explicitly.

```
$fields->fieldByName('Root.Main.Image')->setFolderName('images/page-images')->useMultisitesFolder();
```

The above call to useMultisitesFolder() will change the folder name from 'images/page-images' to 'currentsitesubfolder/images/page-images'

## Known issues

* See [GitHub](https://github.com/sheadawson/silverstripe-multisites/issues?state=open)
