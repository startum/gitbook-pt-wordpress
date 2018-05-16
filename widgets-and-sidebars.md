---
description: Folder 07
---

# Widgets & Sidebars

One of the advantages of using WordPress as your content management system is the extensive widget functionalities the platform offers. If you go to the customizer, navigate to widgets, and the sidebar, and click add widget, you'll see a list of all the available widgets that come with WordPress out of the box, and a lot of these are useful for different purposes. We have things like a search widget, that adds a search form. Recent posts and comments, which adds lists that people can navigate to. We can also create custom menus, add login functionality, etc.

In addition to what ships out of the box, you can also add new widgets using different plug-ins. These widgets are added to widget areas, traditionally in sidebars and footers, and those areas are managed here, from the customizer. In this chapter, we'll take a closer look at both these widget areas and the widgets themselves to make them display and work the way we want them to. 

If we look in functions.php, you'll see the function for adding a widget area to your theme:

```php
/**
 * Register widget area.
 *
 * @link https://developer.wordpress.org/themes/functionality/sidebars/#registering-a-sidebar
 */
function friendsofdesign_widgets_init() {
	register_sidebar( array(
		'name'          => esc_html__( 'Sidebar', 'friendsofdesign' ),
		'id'            => 'sidebar-1',
		'description'   => esc_html__( 'Add widgets here.', 'friendsofdesign' ),
		'before_widget' => '<section id="%1$s" class="widget %2$s">',
		'after_widget'  => '</section>',
		'before_title'  => '<h2 class="widget-title">',
		'after_title'   => '</h2>',
	) );
}
add_action( 'widgets_init', 'friendsofdesign_widgets_init' );
```

Underscores comes shipped with one widgetized area, as you can see above, this widget area is called Sidebar. If we wanted to add another widget area, we would copy the register sidebar function and place directly underneath. For example:

```php
/**
 * Register widget area.
 *
 * @link https://developer.wordpress.org/themes/functionality/sidebars/#registering-a-sidebar
 */
function friendsofdesign_widgets_init() {
	register_sidebar( array(
		'name'          => esc_html__( 'Sidebar', 'friendsofdesign' ),
		'id'            => 'sidebar-1',
		'description'   => esc_html__( 'Add widgets here.', 'friendsofdesign' ),
		'before_widget' => '<section id="%1$s" class="widget %2$s">',
		'after_widget'  => '</section>',
		'before_title'  => '<h2 class="widget-title">',
		'after_title'   => '</h2>',
	) );
        register_sidebar( array(
		'name'          => esc_html__( 'Footer', 'friendsofdesign' ),
		'id'            => 'footer-1',
		'description'   => esc_html__( 'Add widgets here.', 'friendsofdesign' ),
		'before_widget' => '<section id="%1$s" class="widget %2$s">',
		'after_widget'  => '</section>',
		'before_title'  => '<h2 class="widget-title">',
		'after_title'   => '</h2>',
	) );
}
add_action( 'widgets_init', 'friendsofdesign_widgets_init' );

```

We've now added a widget area called Footer to our theme. However, we need to place a bit of php code to the theme so that it shows on the front end of the site. If you open up single.php and scroll to the bottom, you will see a hook get sidebar. We can change this to the footer sidebar we've just created, and then we can style as much as we want to.

Go ahead and try to style your widgets according to your theme. If you add the monster widgets, it will pull up all the available widgets and then you can each one individually. 



