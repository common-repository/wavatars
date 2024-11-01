=== Wavatars ===
Contributors: shamusyoung
Donate link:
Tags: comments, gravtars, icons, avatars
Requires at least: 2.0.2
Tested up to: 2.3.1
Stable tag: trunk

Wavatars will generate and assign icons to the visitors leaving comments at your site.  It can optionally show Gravatars as well.

== Description ==

Wavatars is a plugin that will generate and assign icons to the visitors leaving comments at your site. The icons are based on email, 
so a given visitor will get the same icon each time they comment.  It livens up comment threads and gives people memorable "faces" to 
aid in following conversations.  It's also fun.

<h2>Features:</h2>

<ol>
<li>Wavatars can generate 956,384 different shapes in 57,600 different color combinations for a total of 55,087,718,400 (55 billion)
unique Wavatars.  Yeah, you should have plenty.  You'll run out of human beings (or hard drive space) long before you run out of 
Wavatars.</li>

<li>The icons are generated on-the-fly.  You can adjust the desired size of the icons.</li>

<li>For easy deployment, icons will automatically precede the commenter's name.  You can set HTML to come directly before and after the
icon (to put it inside of a &lt;DIV&gt; tag, for example) or you can control the placement of the icons manually if you don't mind adding 
a single line of PHP to your theme.</li>

<li>Wavatars are based entirely on email and are thus very portable.  The same email will result in the same Wavatar, even on different
sites, so users will have the same icon on all Wavatar-enabled sites.  (Assuming, or course, that there <b>are</b> other Wavatar-enabled 
sites.  I don't know if anyone will want this plugin or not.)</li>

<li>This plugin also supports <a href="http://site.gravatar.com/">Gravatars</a>.  If you like, it can show the Gravatar for a given user 
(if available) and fall back on their Wavatar only if they don't have a Gravatar set up.  This means users can choose to set up a unique 
icon for themselves, and if they don't, they will be assigned a unique Wavatar.  This is a great system that lets people personalize if 
they want, yet still provide a decent icon for the lazy or apathetic.</li>
</ol>

== Installation ==

<ol><li><a href="http://www.shamusyoung.com/files/wavatars1-0-0.zip">Download</a> the plugin.
</li><li>Copy it onto your website in the wordpress <code>/plugins</code> folder.  Then enable the plugin.  That's it. Wavatars will 
instantly appear for all posts (even old ones) on your blog.  If you don't like how the image looks within your theme, read on...
</li></ol>

The administration panel is under Options &raquo; Wavatars.  You can adjust the size of the Wavatars, and assign HTML to come before and 
after each image to help nudge it into place.  Each image is also set with the CSS "wavatars" class.  On my own site, I don't have any 
HTML prefix or suffix, and instead just added these lines to my CSS:

<code>
.wavatar {
	float:             left;
	padding:           3px;
	background:        #fff;
	margin-top:        -25px;
	margin-left:       -25px;
	margin-right:      5px;
}
</code>

If that <i>still</i> doesn't give you enough control over wavatar placement and you don't mind editing your theme, just turn off automatic 
placement and add the line <code>wavatar_show($comment->comment_author_email);</code> to your comment loop wherever you want the image to appear.

Your mileage may vary.  How it will look depends largely on your current theme.

Note that the plugin requires that your install of PHP support the GD library.  If it doesn't, the Wavatars won't show up and you'll get
a warning in the Wavatar admin panel.  You can still use this plugin to display Gravatars, even if the GD library isn't available.

== Screenshots ==

1. A random selection of Wavatars.

== Revision History ==


<h3>Version 1.1.3</h3>

* Fixed bad encoding which would prevent wavatars from appearing if the rating was NOT blank. If the admin does not specify a rating, the rating field is omitted.
* Fixed a typo on the admin panel.
* The wavatar url is now URL encoded.
* The image tag no longer uses the pointless "border tag, and it is now properly closed.
* Removed extra (pointless, harmless) repeated calls to strtolower ().

Thanks to Gavin Lambert for many of these changes.

<h3>Version 1.1.2</h3>

* Made several small changes to comply with the changes at gravatars.com.  Appended .jpg to the $md5 hash, switched to using the new (shorter) field names.
* Fixed bug where the plugin was inserting wavatars in places it shouldn't, such as RSS comment feeds and in sidebar wigits.  The auto-placement will now ONLY place
icons when viewing a single post or a page.
* When placing icons manually within their theme, users should use <code>wavatar_show($comment->comment_author_email)</code> as opposed to
<code>wavatar_show($comment_author_email)</code>, as the eariler versions directed.  The latter will work in some situations but fail in others, and so the former is more correct.
The readme and the admin panel have been updated to reflect this.
* The admin panel will now list how many wavatars are in the cache.

<h3>Version 1.1.0</h3>

* Fixed bug where setting AVATAR_SIZE to an odd number would cause PHP to pass floating-point values to imagefill (), which is not a good idea.
* Fixed bug where gravatars were always requested at 60x60, instead of the size defined in the admin panel.
* Added the function wavatar_get (email, size), which will return the url of the requested avatar instead of displaying it.  This can be useful if you want to use the
image in other ways, such as making it the background of an HTML element.  You could also use this if you need to display the image in a rectangular area instead of a square.
* Added option for controlling the rating of gravatars. (G, PG, R, X)
* Added options for how to handle users who leave the email field blank.  You can choose to give them a wavatar anyway, to give them a blank image, or show no image at all.
* The link back to the wavatars homepage in the footer is now actually a link and not just text.

<h3>Version 1.0.1</h3>

* Initial release.

== Advanced Tricks ==

= Using wavatar_show () =

If you place Wavatars by calling wavatar_show () manually, note that you can also specify an optional "size" argument to override the
default. For example:

<code>wavatar_show($comment->comment_author_email, '160');</code>

This would cause the Wavatar to be 160x160 pixels, even if the default was set to some other value.  You could do this to make admin icons
larger, for example.

= Using wavatar_get () =

If wavatar_show () STILL doesn't give you enough control, you can call:

<code>wavatar_get(email, size);</code>

And it will return the URL to the created image without writing anything to the page.

= Random Wavatar Field =

Put this code in your theme:
<code>
for ($i = 0; $i < 100; $i++)
    wavatar_show ($i);
</code>

It will generate a field of 100 random wavatars, which is amusing.  This is how I generated the wavatar screenshot.  It's also a great way to quickly
test you source images if you're editing the composite parts to make new wavatar types.


