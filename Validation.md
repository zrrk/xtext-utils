With Xtext 2.0 the plugin org.eclipse.xtext.xtend and the `CheckFragment` have been removed. It is recommended to use Java based validation instead of Xpand's Check language, since the interpreted Check languages is poorer in performance, which is crucial for good user experience with Xtext based editors.

However, sometime you might have created a reasonable set of Checks and might want to migrate to Xtext 2 without the direct need to migrate also your validation rules.

The plugin 'org.eclipselabs.xtext.xtend' contains the classes from the plugin of the same name from Xtext <= 1.0.2. Additionally the `CheckFragment` and all its dependencies where copied from 'org.eclipse.xtext.generator' and adapted to Xtext 2.

## Configuration ##

Add a dependency to 'org.eclipselabs.xtext.xtend' to your Xtext runtime project.

Add the `CheckFragment` to your .mwe2 workflow:
```
component = Generator {
   ...
   language = {
      fragment = org.eclipselabs.xtext.generator.validation.CheckFragment {}
   ...
   }
}
```