Backbone Developer Tools
========================

BDT is an extension for Chrome Developer Tools which helps in debugging Backbone-based apps.
It's been developed by [Tomasz Szczęśniak-Szlagowski][1] and released under the [MIT License][2].
It makes use of [Backbone.Debug][3] by Andrew Terris.

Pull requests are welcome!

Features
--------

* $view console variable after inspecting a DOM Element (points to the closest View instance)
* Containing Views Hierarchy in Elements panel
* Logs in Backbone Panel:
  * Events
  * Syncs
  * View-DOM Binding
  * Instantiated Objects

Installing
----------

### Web Store

BDT is yet to be released, so you need to install it manually.

### Manually

1. Clone this repo
2. Go to *Tools -> Extensions* in Google Chrome
3. Check *Developer mode* and click *Load unpacked extension*
4. Choose the cloned repo directory


Usage
--------

1. Open a new tab (for first time users)
2. Open the Chrome Dev Tools
3. Go to the Backbone Tab (Usually it will be near the *Console* tab)
4. Make sure that *Inject Backbone.Debug (changing this will cause a page reload)* has been checked
5. Create a new bookmark and add the following as its contents/url:
<pre>
javascript:(function(){var o=window.$view;if(!o)return;\_.each(['Adroll.Collections','Adroll.Models','Adroll.Views','Dashboard.Collections','Dashboard.Models','Dashboard.Views'],function(ns){var parts=ns.split('.'),v=window;\_.each(parts,function(p){v=v[p]});\_.each(v,function(k,n){if(\_.isFunction(k)&&o instanceof k){var p=' ';if(Object.getPrototypeOf(o)===k.prototype)p='*';console.log(p+ns+'.'+n);}});});})();
</pre>
6. Now when you *Inspect Element*, you can click on this bookmarklet and check the console for the view name.



Known Limitations
-----------------

By default, Backbone Developer Tools require *window.Backbone* to be available on DOMContentLoaded. We have a fallback method for asynchronously loaded Backbone that seems to work pretty well, too.

If neither the default nor the fallback succeed in injecting Backbone Developer Tools, you can modify *js/inject/attach.js* to meet your specific requirements.

You could also try modifying *js/inject/logger.js* and *js/inject/backbone.debug.js* and including them by yourself.
Note that unless you alter the extension itself, you'll need to expose the logger at *window.Backbone.debug.logger*.


[1]: http://github.com/spect88
[2]: http://www.opensource.org/licenses/MIT
[3]: http://github.com/aterris/backbone.debug
