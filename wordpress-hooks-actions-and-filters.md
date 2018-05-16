# WordPress Hooks - Actions & Filters

Hooks are what make WordPress so powerful for developers. Basically, when the coders who designed WordPress wrote the code, they inserted in hundreds of places where other developers could add in their own custom functionality. In order to do any heavy customization of WordPress, you'll need to interact with hooks at some level. 

Two types of hooks exist in WordPress, actions and filters. 

Actions let you insert your own code to run at different points while WordPress is running. For example, run my code when a post is saved, or run my code when a menu is loaded. Filters on the other hand, let you modify content in WordPress. For example, add a custom footer to the end of the main content of a post, or limit the excerpt of a post to a certain number of characters. Let's look at a few common examples of where you would use hooks in WordPress. 

Lets open up our functions.php file, again right at the end of our 2015 theme setup function, which starts up here, and then ends where this curly brace ends right here, we can see add action, after setup, 2015 setup. 

```php
	add_theme_support( 'custom-background', apply_filters( 'twentyfifteen_custom_background_args', array(
		'default-color'      => $default_color,
		'default-attachment' => 'fixed',
	) ) );

	/*
	 * This theme styles the visual editor to resemble the theme style,
	 * specifically font, colors, icons, and column width.
	 */
	add_editor_style( array( 'css/editor-style.css', 'genericons/genericons.css', twentyfifteen_fonts_url() ) );

	// Indicate widget sidebars can use selective refresh in the Customizer.
	add_theme_support( 'customize-selective-refresh-widgets' );
}
endif; // twentyfifteen_setup
add_action( 'after_setup_theme', 'twentyfifteen_setup' );
```

What this is doing, is taking our function that we wrote and tying it into one of the WordPress hooks, specifically a hook called after set up theme. So what that means is that after WordPress goes ahead and does everything it needs to do to set up a theme, we're telling WordPress, let us hook our special set up function into your code when you're setting up this theme. 

If we come down to the widgets, we can see that 2015 widgets\_init is being hooked into the widgets\_init action hook. 

```php
function twentyfifteen_widgets_init() {
	register_sidebar( array(
		'name'          => __( 'Widget Area', 'twentyfifteen' ),
		'id'            => 'sidebar-1',
		'description'   => __( 'Add widgets here to appear in your sidebar.', 'twentyfifteen' ),
		'before_widget' => '<aside id="%1$s" class="widget %2$s">',
		'after_widget'  => '</aside>',
		'before_title'  => '<h2 class="widget-title">',
		'after_title'   => '</h2>',
	) );
}
add_action( 'widgets_init', 'twentyfifteen_widgets_init' );
```

Again at the end of our other functions like this scripts functions that's loading all the CSS and JS, we could see that we're calling our function and adding it to wp\_enqueue\_scripts. 

```php
add_action( 'wp_enqueue_scripts', 'twentyfifteen_scripts' );
```

This hook is enqueuing all the CSS and JavaScript that WordPress needs to use on the front end and lets us also tie in our own code. We can see here that this is another one that's tying in to something similar, and here we see one that's not tying into an action hook, but a filter, and what this is doing is it's doing a string replace. 

```php
function twentyfifteen_search_form_modify( $html ) {
	return str_replace( 'class="search-submit"', 'class="search-submit screen-reader-text"', $html );
}
add_filter( 'get_search_form', 'twentyfifteen_search_form_modify' );
```

When it gets the search form, it's changing how it displays and what it displays, and writing it into a custom function so that when WordPress goes to get the search form, it's going to display slightly different and customize specifically how the 2015 theme wants it to be. 

On the WordPress codex, we have a special page that lists out all of the hooks that WordPress offers. 

```text
https://codex.wordpress.org/Plugin_API#Hooks.2C_Actions_and_Filters
```

Broken into the two types of either filters or actions. If we open these up, we could see a list of all of the possible filters that WordPress has split out by posts and pages, comments, categories, links, dates, authors, blog information, etc., etc. 

So basically, any information that WordPress is outputting related to ny of these, we could write our own custom function and hook it in to customize what's happening inside of WordPress. The action reference is done the same way and it's split into these different categories and gives some basic information about each hook. However, these ones that are in red mean that there's not anything about this yet in the Codex. However, you should be able to find some good information on the most common types of hooks that you would use in WordPress and how to call them and what they do.





