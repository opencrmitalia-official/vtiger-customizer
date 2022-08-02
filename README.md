# Vtiger Customizer

> What is the Vtiger Customizer?

The Vtiger Customizer is a technique to extends Vtiger Core functions and methods without change core files but just define new functions and bind or connect it (the new function) to the original one.

> Did you explain it with an example?

Imagine you need a plugin that change the behaviour of `Vtiger_Module_Model::getModuleIcon()`

Instead of change the code inside of it you can do this:

```
Vtiger_Customizer::extendMethod('Vtiger_Module_Model::getModuleIcon', function() {
  return '<span class="my-icon"></icon>';
});
```

With this, everytime the Vtiger core call this method your custom version runs instead the original one.

> Why I need this?

As "Vtiger Module Developer" I need some special behaviours and essentially I need a way to customize the core or override core methods without rewrite core files.

For examples:

- Customize the Subject of a mail for every emails the CRM sends
- Customize the List View query withoud hardcode the file List.php
- Customize the get_related methods to supports filters

> Did Customizer is a extension framework?

Yes, it enable Vtiger Module/Extension Developer to add behaviour without replace core files.
