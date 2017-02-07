<h3 align="center">PMkit documentation draft v1.1<sup><a href="#note1">[1]</a></sup></h3>

* PMkit is an experimental Pale Moon library that provides basic compatibility layer with [Mozilla Add-on SDK](https://developer.mozilla.org/en-US/Add-ons/SDK). It implements the most of the API but has the differences described below in the document. Thus, to successfuly run in Pale Moon, the extensions initially targeted to the other browsers (such as Firefox or SeaMonkey) should be properly adapted.

* PMkit supports only the add-ons created using [jpm](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/jpm). The old style (cfx) extensions should be first [migrated](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/cfx_to_jpm) to jpm to be able to run in Pale Moon. Use "*{8de7fcbb-c55c-4fbe-bfc5-fc555c87dbc4}*" as a name of engine and "*27.1.0b1*" as a minimal version to add Pale Moon as a target application in *[package.json](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/package_json#Creating_a_manifest)*<sup><a href="#note2">[2]</a></sup>. If you prefer to create *[install.rdf](https://developer.mozilla.org/en-US/Add-ons/Install_Manifests#targetApplication)* manually, you also have to set *targetApplication* using the above values. This will allow to use jpm to build, test, run and debug as usual.

* PMkit has some limitations and supplements. The rarely used modules "*ui/frame*", "*ui/sidebar*" and "*ui/toolbar*" are currently unsupported, although it may be changed in the future. This also applies to all API that were or will be added to Mozilla Add-on SDK after Gecko 38. Since Pale Moon does not use separate processes for browser's UI and web content (e10s) and does not support WebExtensions the corresponding "*remote/parent*", "*remote/child*" and "*webextension*" modules are absent in PMkit completely. At the same time, the "*widget*" module, that was removed from Mozilla Add-on SDK, can still be used with PMkit to create buttons, along with "*ui/button/action*" and "*ui/button/toggle*" (please always include 16px icon for the last ones).

* You should also take into account that Pale Moon uses his own browser core named Goanna. The main differences from Mozilla products that follow from this are described in a [separate document](http://www.palemoon.org/technical.shtml#Firefox_Differences). So, any routines not related to SDK must be also brought into line with the target environment.

* Despite the experimental status of PMkit, several popular add-ons have already been successfully adapted and work fine in Pale Moon. Some of them run even faster and use less memory than in the browser for which they were originally created. Nevertheless, traditional bootstrapped and XUL extensions remain the preferred and most optimal types of add-ons for Pale Moon.

<a name="note1">[1]</a> This document is currently applicable to [Pale Moon 27.1.0b1 and above](https://forum.palemoon.org/viewtopic.php?f=1&t=14455).

<a name="note2">[2]</a> Example of *package.json* for add-on that is targeted to both Firefox and Pale Moon:
```
{
  "name": "my-addon",
  "title": "my-addon",
  "id": "jid1-1FERGV45e4f4f@jetpack",
  "description": "a basic add-on",
  "author": "",
  "license": "MPL-2.0",
  "version": "0.1",
  "engines": {
    "firefox": ">=38.0a1",
    "{8de7fcbb-c55c-4fbe-bfc5-fc555c87dbc4}": ">=27.1.0b1"
   }
}
```
