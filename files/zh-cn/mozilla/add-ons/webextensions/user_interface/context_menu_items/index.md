---
title: Context menu items
slug: Mozilla/Add-ons/WebExtensions/user_interface/Context_menu_items
---
{{AddonSidebar}}

This user interface option adds one or more items to a browser context menu. This is the context menu available when a user right-clicks on a web page. Tabs can have context menus also, available through the [browser.menus API](/en-US/Add-ons/WebExtensions/API/menus).

![Example of content menu items added by a WebExtension, from the context-menu-demo example](context_menu_example.png)

You would use this option to expose features that are relevant to specific browser or web page contexts. For example, you could show features to open a graphic editor when the user clicks on an image or offer a feature to save page content when part of a page is selected. You can add plain menu items, checkbox items, radio button groups, and separators to menus. Once a context menu item has been added using {{WebExtAPIRef("contextMenus.create")}} it's displayed in all browser tabs, but you can hide it by removing it with {{WebExtAPIRef("contextMenus.remove")}}.

## Specifying context menu items

You manage context menu items programmatically, using the {{WebExtAPIRef("contextMenus")}} API. However, you need to request the `contextMenus` permission in your manifest.json to be able to take advantage of the API.

```json
"permissions": ["contextMenus"]
```

You can then add (and update or delete) the context menu items in your extension's background script. To create a menu item you specify an id, its title, and the context menus it should appear on:

```js
browser.contextMenus.create({
  id: "log-selection",
  title: browser.i18n.getMessage("contextMenuItemSelectionLogger"),
  contexts: ["selection"]
}, onCreated);
```

Your extension then listens for clicks on the menu items. The passed information about the item clicked, the context where the click happened, and details of the tab where the click took place can then be used to invoke the appropriate extension functionality.

```js
browser.contextMenus.onClicked.addListener(function(info, tab) {
  switch (info.menuItemId) {
    case "log-selection":
      console.log(info.selectionText);
      break;
    ...
  }
})
```

## Examples

The [webextensions-examples](https://github.com/mdn/webextensions-examples) repo on GitHub, contains several examples of extensions that use context menu items:

- [menu-demo](https://github.com/mdn/webextensions-examples/tree/master/menu-demo) adds several items to the browser's context menu.
- [context-menu-copy-link-with-types](https://github.com/mdn/webextensions-examples/tree/master/context-menu-copy-link-with-types) adds a context menu item to links that copies the URL to the clipboard, as plain text and rich HTML.
