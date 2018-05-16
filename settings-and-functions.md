# Settings & Functions

Lets open up our functions.php file from your theme. 

Underscores is a bare bones parent theme, so they've left a lot of comments in the files to show you what these particular functions do. 

Lets go through a few of these functions:

First up are the various different theme supports.  There are a number of these, but the ones we're going to concentrate on are the following:

Post Thumbnails - Add feature images to your theme.

Menus - One registered nav menu. The array is only holding one menu right now.

Background Feature - Hooks into the customizer and allows a function to change the background color in the customizer.

$GLOBALS\['content\_width'\] - All content such as youtube videos and embedded content will have a width of 640. 

Widgets - Register sidebar adds a widgetized area. 

Enqueue Styles - Loads the stylesheets and scripts for your theme. 

We're going to now add custom fonts to our theme, and we're going to do it with the enqueue function. 

Lets go to Google Fonts and grab the following fonts:

**Quicksand Bold**

**Catamaran Bold 700**

**Muli Regular**

All we now have to do is queue up a custom style sheet, and then call for the font in the CSS. Grab the URL from the stylesheet href and copy it. Then open your functions.php and find the enqueue section. Just after the opening curly bracked for the function scripts, paste the following code:

```php
 wp_enqueue_style( 'friendsofdesign-fonts', 'https://fonts.googleapis.com/css?family=Catamaran:700|Muli|Quicksand:700' );
```

Save the file and go back to your browser. If you view page source, you should now be able to see that style sheet being linked. 

Now we need to apply the styles. Typography is located in the sass &gt; variables-site folder. The variables folder is where we're going to find all our variables for styling with sass. 

In this file, lets create 3 new variables:

$font-heading

$font-subheading

And add the custom font to our $font-main variable

Each of these variables will need a value, so go ahead and add the various fonts you want for each of these variables.

```css
$font-heading: 'Catamaran', sans-serif;
$font-subheading: 'Quicksand', sans-serif;
$font-main: 'Muli', sans-serif;
```

Lets now apply these variables to our styles. We need to add them is in the typography folder, and then headings.scss

```css
h1, h2 {
	clear: both;
        font-family: $font-heading;
}

h3, h4, h5, h6{
	clear: both;
        font-family: $font-subheading;
}
```

If we now go to our browsers, you will see that the fonts have now been applied. 





