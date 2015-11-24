# backbone.marionette.keyshortcuts
An extension to `Backbone.Marionette.View` that adds a `keyShortcuts` hash to the view object, allowing you to register keyboard commands using `Mousetrap.js`.

# Dependencies
 * Marionette https://github.com/marionettejs/backbone.marionette
 * Moustrap https://github.com/ccampbell/mousetrap
 
# Installation
    npm install backbone.marionette.keyshortcuts

If you are using `requireJS` then you need to ensure that `mousetrap` can be found on the default path, or is defined in your require config.
```` javascript
    paths: {
      'backbone.marionette.keyShortcuts': '/vendor/marionette/backbone.marionette.keyshortcuts',
      'mousetrap':'/vendor/mousetrap/mousetrap.min'
    }
````

# Usage

In your `View` class, simply add a `keyShortcuts` like you would for the `events` hash.

It supports single keys and key combinations. To define the event trigger, add a double colon, followed by the event name after your key combination; `'d::keyup'`.
```` javascript
View.MyForm = Marionette.ItemView.extend({
 tagName: 'form',
 keyShortcuts:{
  'command+s' : 'save',
  'up up down left' : function() { console.log('cheat!') },
  'd::keyup' : function() { console.log('d key was released') },
 },
 events: {
  'click @saveBtn' : 'save',
 },
 ui: {
  'saveBtn' : '.save'
 },
 save: function(e) {
  e.preventDefault(); //stop the browser saving..
  this.model.save();
 }
});
````
Or you can define them in a `Behavior` class
```` javascript   
ShortcutsBehaviour = Marionette.Behavior.extend({
 keyShortcuts: {
  "backspace": "delete",
  "del": "delete"
 },
 
 delete:functio(e) {
  e.preventDefault(); //stop the browser from navigating back
  console.log("Delete something!");
 }
}
````   
````javascript

View.MyForm = Marionette.ItemView.extend({
 tagName: 'form',
 behaviors: {
  ShortcutsBehaviour: {
   behaviorClass: ShortcutsBehaviour
  }
 },
});
````

# Info
See https://craig.is/killing/mice for how to use Mousetrap.
