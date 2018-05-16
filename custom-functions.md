# Custom Functions

A function in PHP is a block of code that can be reused and execute whatever programming logic you need it to. Custom functions are more common in advanced theme development and plugin development.

When you're creating custom themes or plugins, you'll often have to start writing your own PHP code. This code is often stored in custom functions. A function is a block of code that can be used again and again and called whenever you need. 

When it comes to looking for examples of functions in WordPress, one of the go to places to look for themes is inside of the functions.php file. Let's look at the functions.php in twentyfifteen theme. 

We'll see it opens with a PHP block and then comes down, and we can see the word function, the name of a function, parentheses, and then an open curly brace that will close at the end of the function. This is how we know that we're working with a function. We see the word function, and then the name of the function written out, parentheses, and curly braces. Sometimes, functions will have parameters, or things passed to them, inside of them, that let them be customized, but sometimes they're just simple functions like this. 

When building a custom theme, functions are one of the things that you'll go into in a lot of depth. We're going to look at some  ways that functions are commonly used, specifically, when working with theme development. 

Now we could see from this name that this is helping to set up the 2015 theme and when we come down we could see it's doing things like adding theme support for things like the title tag, post thumbnails, setting default post thumbnail sizes, registering navigation menus, adding theme support for html5 in different ways. For post-formats, setting color scheme values, as well as some other things. If we come down and look at more functions we could see that this one is initializing widgets. So this is setting up a sidebar area that allows us to add widgets to it. 

We have one dealing with fonts, and then a very common one that shows how to link to CSS and JS.  We're calling other functions to add in style sheets as well as different types of JavaScripts. We could see they're even using conditional statements to only load certain scripts. 

```php
function twentyfifteen_scripts() {
	// Add custom fonts, used in the main stylesheet.
	wp_enqueue_style( 'twentyfifteen-fonts', twentyfifteen_fonts_url(), array(), null );

	// Add Genericons, used in the main stylesheet.
	wp_enqueue_style( 'genericons', get_template_directory_uri() . '/genericons/genericons.css', array(), '3.2' );

	// Load our main stylesheet.
	wp_enqueue_style( 'twentyfifteen-style', get_stylesheet_uri() );

	// Load the Internet Explorer specific stylesheet.
	wp_enqueue_style( 'twentyfifteen-ie', get_template_directory_uri() . '/css/ie.css', array( 'twentyfifteen-style' ), '20141010' );
	wp_style_add_data( 'twentyfifteen-ie', 'conditional', 'lt IE 9' );

	// Load the Internet Explorer 7 specific stylesheet.
	wp_enqueue_style( 'twentyfifteen-ie7', get_template_directory_uri() . '/css/ie7.css', array( 'twentyfifteen-style' ), '20141010' );
	wp_style_add_data( 'twentyfifteen-ie7', 'conditional', 'lt IE 8' );

	wp_enqueue_script( 'twentyfifteen-skip-link-focus-fix', get_template_directory_uri() . '/js/skip-link-focus-fix.js', array(), '20141010', true );

	if ( is_singular() && comments_open() && get_option( 'thread_comments' ) ) {
		wp_enqueue_script( 'comment-reply' );
	}

	if ( is_singular() && wp_attachment_is_image() ) {
		wp_enqueue_script( 'twentyfifteen-keyboard-image-navigation', get_template_directory_uri() . '/js/keyboard-image-navigation.js', array( 'jquery' ), '20141010' );
	}

	wp_enqueue_script( 'twentyfifteen-script', get_template_directory_uri() . '/js/functions.js', array( 'jquery' ), '20150330', true );
	wp_localize_script( 'twentyfifteen-script', 'screenReaderText', array(
		'expand'   => '<span class="screen-reader-text">' . __( 'expand child menu', 'twentyfifteen' ) . '</span>',
		'collapse' => '<span class="screen-reader-text">' . __( 'collapse child menu', 'twentyfifteen' ) . '</span>',
	) );
}
add_action( 'wp_enqueue_scripts', 'twentyfifteen_scripts' );
```

For example, the comment-reply JavaScript only on pages that are singular page with comments open. 

```php
if ( is_singular() && comments_open() && get_option( 'thread_comments' ) ) {
		wp_enqueue_script( 'comment-reply' );
	}
```

Sometimes, themes will load in specific things that only apply to that theme. For example, widgets are used in a lot of themes, but not all themes would have custom post navigation backgrounds. 

If we scroll, we can see a number of different functions being used here. These functions may just be used once in our functions.php file, or they may be called directly in templates depending on the need for them. 

```php
/**
 * Implement the Custom Header feature.
 *
 * @since Twenty Fifteen 1.0
 */
require get_template_directory() . '/inc/custom-header.php';

/**
 * Custom template tags for this theme.
 *
 * @since Twenty Fifteen 1.0
 */
require get_template_directory() . '/inc/template-tags.php';

/**
 * Customizer additions.
 *
 * @since Twenty Fifteen 1.0
 */
require get_template_directory() . '/inc/customizer.php';
```

We could see we're also including some other files down here using the require get\_template\_directroy, and then the name of the file that they want to include. 

Now writing a function on its own doesn't do much in WordPress, what we need to be doing is tying in to what are called hooks. 

