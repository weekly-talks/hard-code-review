Sometimes there is code on review which works but it is not clean. This code puts reviewer into a dilemma. Should we merge this code and plan refactoring for later. Or should we veto merge and ask developer to fix that code?

## Code in question

```diff
     // ...
     
     return this.get('savedModels').filter(model =>
-        model.get('modelName') === search ||
-        model.get('uniqueId') === search ||
-        model.get('subtypeName') === search ||
-        model.get('manufacturerName') === search ||
-        model.get('meterReads') === search ||
-        model.get('modelYear') + '' === search
+      (model.get('modelName') + '/\n' +
+      model.get('uniqueId') + '/\n' +
+      model.get('subtypeName') + '/\n' +
+      model.get('manufacturerName') + '/\n' +
+      model.get('meterReads') + '/\n' +
+      model.get('modelYear') + '/\n').indexOf(search) >= 0
     );
```
