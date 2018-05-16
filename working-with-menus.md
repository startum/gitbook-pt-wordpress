---
description: folder 04
---

# Working with Menus

A menu in WordPress has two components. First it will need to be registered in the back end of WordPress as a menu that can be customized either in the customizer or from the dashboard itself.Then, it has to be added into the theme so it will be displayed. This is done using two different functions. First, register\_nav\_menus which registers the menu into WordPress so WordPress knows it's available and adds it to the customizer as a location. 

```php

register_nav_menus( array(	'pluginbuddy_mobile' => 'PluginBuddy Mobile Navigation Menu',	'footer_menu' => 'My Custom Footer Menu',) );
```

Second, wp\_nav\_menu is the function that's used to display the menu on the front end. A wp\_nav\_menu has a ton of parameters you can use to customize the output of the menu. We're not going to go through all the parameters, but take through the codex to get more of an idea: [https://developer.wordpress.org/reference/functions/wp\_nav\_menu/](https://developer.wordpress.org/reference/functions/wp_nav_menu/)

```php
wp_nav_menu( array(
    'theme_location' => is_user_logged_in() ? 'logged-in-menu' : 'logged-out-menu'
) );
```

In the example above, a menu called 'logged-in-menu' will only show if the user is logged in, else it will show the menu 'logged-out-menu'.

First off, lets register a new menu called 'Secondary'. In our functions.php file you'll find a line of code that says 'register nav'. All we need to do is copy that line of code and paste underneath it, then change the relevant info:

```php
// This theme uses wp_nav_menu() in one location.
	register_nav_menus( array(
		'primary' => esc_html__( 'Primary', 'friendsofdesign' ),
        'secondary' => esc_html__( 'Secondary', 'friendsofdesign' ),
	) );
```

Great, remember to click save and if you go to your menu options, you'll now see a new menu location called Secondary. Lets actually take that secondary menu out for the moment and change the name of the primary menu to Header. 

```php
// This theme uses wp_nav_menu() in one location.
	register_nav_menus( array(
		'header' => esc_html__( 'Header', 'friendsofdesign' ),
	) );
```

So the functionality is there, but how do we get it to display? We need to go into our header.php. At the bottom of the file you'll see there wp nav menu option. Lets go ahead and change all this information to fit the nav we've just registered.

```php
<nav id="site-navigation" class="main-navigation" role="navigation">
			<button class="menu-toggle" aria-controls="primary-menu" aria-expanded="false"><?php esc_html_e( 'Header Menu', 'friendsofdesign' ); ?></button>
			<?php wp_nav_menu( array( 'theme_location' => 'header', 'menu_id' => 'header-menu' ) ); ?>
		</nav><!-- #site-navigation -->
```

Lets now style our menu. 

WordPress automatically places menu items in a float, which causes a number of issues, so we're going to change this to flexbox. This means that we don't have to put in clear floats and other niggly things to get the menu to work the way we want it to. 

Underscores ships with their own custom styles, so we're going to over ride these styles now. Open up your sass folder &gt; navigation &gt; menus.scss. Delete everything so you're only left with the following:

```css
.comment-navigation,
.posts-navigation,
.post-navigation {

	.site-main & {
		margin: 0 0 1.5em;
		overflow: hidden;
	}

	.nav-previous {
		float: left;
		width: 50%;
	}

	.nav-next {
		float: right;
		text-align: right;
		width: 50%;
	}
}
```

Great, now lets add our own styles. Create a document in your header folder called header-menu.scss. Then head over to your header.scss and import that document:

```css
/*
Header Menu
*/
@import "header-menu";
```

Then add the following styling to your header-menu.scss file:

```css
.main-navigation {
	display: block;
	font-family: $font__main;
        font-size: 1em;
	clear: left;
	
	ul {
		display: none;
		list-style: none;
		margin: 0;
		padding-top: 1em;
		padding-left: 0;

		ul {
			display: none;
			top: 1.5em;
			z-index: 99999;

			ul {
				top: 0;
			}

			li {
				padding-left: 1em;                                
                                
				
				&:hover > ul,
				&.focus > ul {
					left: 100%;
				}
			}

			a {
				width: 200px;
			}
		}

		li:hover > ul,
		li.focus > ul {
			left: auto;
		}
	}

	li {
		position: relative;
	}

	a {
		display: inline-block;
		width: 100%;
		padding: .5em 1em .5em 0;
		text-decoration: none;
		color: #000;
	}
	
	a:hover,
	a:focus {
		text-decoration: underline;
	}

	.current_page_item > a,
	.current-menu-item > a,
	.current_page_ancestor > a,
	.current-menu-ancestor > a {
	}
	
	.menu-item-has-children,
	.page-item-has-children {
		min-width: 218px;
	}
	.menu-item-has-children > a,
	.page_item_has_children > a {
		padding-right: 2em;
	}
}

button.dropdown-toggle {
	position: absolute;
	right: 0;
	border: none;
	background: inherit;
	color: white;
	line-height: 1.5em;
	padding: .4em 1em .4em .5em;
}

.menu-toggle {
	position: absolute;
	top: 0;
	right: 0;
	display: block;
	margin: 1.2em 1.2em 0 0;
	padding: .6em .8em;
	font-size: 80%;
	text-transform: uppercase;
	color: white;
	border: 1px solid hsla(0, 0%, 100%, .3);
}

/* Toggle small menu and sub-menus on */
.toggled-on ul,
.sub-menu.toggled-on {
	display: block;
}

@media screen and (min-width: $query__small) {
	.menu-toggle {
		display: none;
	}
	
	.main-navigation {
		
		.menu-item-has-children > a,
		.page_item_has_children > a {
			padding-right: 2em;
			background: hsla(0, 0%, 100%, .1);
		}
		
		ul {
			display: block;
			display: flex;
			flex-wrap: wrap;
			
			ul {
				flex-direction: column;
				background: hsla(0, 0%, 100%, .1);
				margin-left: 0;

				li {
					padding-left: 0;
					
					a {
						width: 218px;
						background: none;
					}
				}
			}
			
			li {
				
				a {
					padding: .4em 1em; 
				}
			}
		}
		
	}
}

@media screen and (min-width: $query__medium) {
	.main-navigation {
		
		ul {
			justify-content: flex-end;
			padding-top: 0;
                        
		}
		
	}
}

```

You can see in the code above that we have styling for the responsive view. We can't see that at the moment as we need to add the javascript to that. 

We're not going to use the javascript that shipped with Underscores, we're going to use the javascript that is available in the twentyseventeen wordpress theme. 

But lets have a look at the current javascript for the drop down and mobile menu. Go to Functions.php and go the script setup, there is a enqueue called friendsofdesign-navigation, its pulling the javascript from the js/navigation.js file. When we look at this file we can see the basics that underscores comes with, but we're going to replace this with the twentyseventeen javascript. 

This is a little bit out of the scope of this course, so go ahead and use the 05 theme in the exercise folders.

Have a look in the themes navigation.js file and the functions.php and see how its now changed. 



