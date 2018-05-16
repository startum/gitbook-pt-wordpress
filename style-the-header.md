---
description: Start with folder 03
---

# Style the header

Its always best to work from the top down with custom themes, and the top in WordPress is the header. Everything you need to know about the header will be located in the header.php file. 

If you look through the header.php file you can see that the structure is the same as a HTML header element. We have the opening head tag, meta tags, link to stylesheets, opening body tag and then the beginning of our header with the opening header tag. 

We're going to work on the header and the site-branding div. 

For the header styles, I've created a header.scss file which is going to contain all the styles that we'll be using for the header. We need to import this stylesheet into the site. We do this by adding the following code to the site.scss file under the secondary folder.

```css
/*--------------------------------------------------------------
## Header
--------------------------------------------------------------*/
@import "header/header";
```

Next we need to add various styles to our header, using the variables that we've created.

```css
.site-header {
    position: relative;
    padding: 2em;
    font-family: $font__main;
    color: #000;
    background-color: grey;
    
    @media screen and (min-width: $query__small) {
        padding: 1em 2em;
    }
}
```

You can see that I've added a variable $query\_\_small for the media query. This variable was added into the structure.scss file. 

Next we need to add styling to the site branding and site title. 

```css
.site-branding{
    min-height: 100px;
}

.site-title{
    margin: 0;
    padding: 0;
    font-family: $font-heading;
    
    a {
        color: #9e9e9e;
        text-decoration: none;
        
        &:hover,
            &:focus {
            text-decoration: underline;
        }
    }
}
```

You can see here that we added a hover state of underline and changed the color of the link. If you go back to your browser you should see a significant change to your site header. 

Lastly we need to style the site description

```css
.site-description {
    margin: 0;
    font-size: .9em;
    font-style: italic;
    font-weight: 100;
}
```

For my design, I want the menu to move to the right handside of the site title, and to do that we're going to utilise flexbox. We need to find out which container is holding both the site title and the menu. This will be .site-header. 

Add the following to your header.scss file:

```css
@media screen (min-width: $query__medium) {
    .site-header {
        display: flex;
        justify-content: space-between;
    }
    
    .site-branding {
        width: 35%;
    }
    
    .site-navigation {
        width: 55%;
    }
}
```

As you see, we've used a variable called $query\_\_medium, but we haven't specified the parameters for that variable. And if you look at your terminal window, you'll see an error showing that very instruction. This is specified in structure.scss under your variables folder. Add the follow variable to that file:

```css
$query__medium: 900px;
```

### Optional Custom Header Image

Open up your WordPress site in a different browser window. If you open up the customizer, you'll see there is an option to add a Header Image, with the header size of 1000 x 250 pixels. But at the moment that functionality is not working. 

We're going to change the settings so that we get the right size image. Then hook the image into the theme so it displays, then we'll apply styling to make it look the way we want it to. 

If we open the functions.php at the very bottom , you can see all the require statements that point at the inc folder. The first required file is inc/custom-header. This is where all the custom header information is defined. So if we go to inc and custom-header, and scroll down, you'll see this is where the custom header is defined.

```php
<?php
/**
 * Sample implementation of the Custom Header feature.
 *
 * You can add an optional custom header image to header.php like so ...
 *
	<?php if ( get_header_image() ) : ?>
	<a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home">
		<img src="<?php header_image(); ?>" width="<?php echo esc_attr( get_custom_header()->width ); ?>" height="<?php echo esc_attr( get_custom_header()->height ); ?>" alt="">
	</a>
	<?php endif; // End header image check. ?>
 *
 * @link https://developer.wordpress.org/themes/functionality/custom-headers/
 *
 * @package friendsofdesign
 */

/**
 * Set up the WordPress core custom header feature.
 *
 * @uses friendsofdesign_header_style()
 */
function friendsofdesign_custom_header_setup() {
	add_theme_support( 'custom-header', apply_filters( 'friendsofdesign_custom_header_args', array(
		'default-image'          => '',
		'default-text-color'     => '000000',
		'width'                  => 1000,
		'height'                 => 250,
		'flex-height'            => true,
		'wp-head-callback'       => 'friendsofdesign_header_style',
	) ) );
}
add_action( 'after_setup_theme', 'friendsofdesign_custom_header_setup' );

if ( ! function_exists( 'friendsofdesign_header_style' ) ) :
/**
 * Styles the header image and text displayed on the blog.
 *
 * @see friendsofdesign_custom_header_setup().
 */
function friendsofdesign_header_style() {
	$header_text_color = get_header_textcolor();

	/*
	 * If no custom options for text are set, let's bail.
	 * get_header_textcolor() options: Any hex value, 'blank' to hide text. Default: HEADER_TEXTCOLOR.
	 */
	if ( HEADER_TEXTCOLOR === $header_text_color ) {
		return;
	}

	// If we get this far, we have custom styles. Let's do this.
	?>
	<style type="text/css">
	<?php
		// Has the text been hidden?
		if ( ! display_header_text() ) :
	?>
		.site-title,
		.site-description {
			position: absolute;
			clip: rect(1px, 1px, 1px, 1px);
		}
	<?php
		// If the user has set a custom color for the text use that.
		else :
	?>
		.site-title a,
		.site-description {
			color: #<?php echo esc_attr( $header_text_color ); ?>;
		}
	<?php endif; ?>
	</style>
	<?php
}
endif;

```

We going to change the width to 2000 and the height to 850 and leave everything else as is.

```php
function friendsofdesign_custom_header_setup() {
	add_theme_support( 'custom-header', apply_filters( 'friendsofdesign_custom_header_args', array(
		'default-image'          => '',
		'default-text-color'     => '000000',
		'width'                  => 2000,
		'height'                 => 850,
		'flex-height'            => true,
		'wp-head-callback'       => 'friendsofdesign_header_style',
	) ) );
}
add_action( 'after_setup_theme', 'friendsofdesign_custom_header_setup' );
```

Next we need to add that functionality to the header.php file, so that the customizer option will work. At the top of the custom-header.php file you'll see the following:

```php
/**
 * Sample implementation of the Custom Header feature.
 *
 * You can add an optional custom header image to header.php like so ...
 *
	<?php if ( get_header_image() ) : ?>
	<a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home">
		<img src="<?php header_image(); ?>" width="<?php echo esc_attr( get_custom_header()->width ); ?>" height="<?php echo esc_attr( get_custom_header()->height ); ?>" alt="">
	</a>
	<?php endif; // End header image check. ?>
```

As you can see by the comments, underscores has shipped this functionality with their theme, so all we need to do is copy and paste it into our header.php. 

Open up your header.php and add the code just above the opening header tag.

```php
?><!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
<meta charset="<?php bloginfo( 'charset' ); ?>">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="profile" href="http://gmpg.org/xfn/11">

<?php wp_head(); ?>
</head>

<body <?php body_class(); ?>>
<div id="page" class="site">
	<a class="skip-link screen-reader-text" href="#content"><?php esc_html_e( 'Skip to content', 'friendsofdesign' ); ?></a>
        
        
            <?php if ( get_header_image() ) : ?>
        <figure class="header-image">
            <a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home">
                    <img src="<?php header_image(); ?>" width="<?php echo esc_attr( get_custom_header()->width ); ?>" height="<?php echo esc_attr( get_custom_header()->height ); ?>" alt="">
            </a>
        </figure>
            <?php endif; // End header image check. ?>

	<header id="masthead" class="site-header" role="banner">
```

 You can see that I've added a figure class to my code, this is so we can style it. Go back to your customizer and add a custom header image. You should be able to see that it is now working. Again, we need to style this, as there is a margin above and below the element. 

In your Sass folder, open your elements folder and then elements.scss. Adjust the figure magin to only be 0px. There is still a margin underneath the image as we need to change the image to a display as a block element. Open up your header.scss file and add the following styles:

```css
.header-image {
    max-height: 60vh;
    overflow: hidden;
    
    img {
        display: block;
        width: 100vw;
    }
}
```

### Adding optional custom logo to the header

Adding a custom logo to the header is done through the customizer, however we need to add that functionality to our theme. We'll be doing that through our functions.php. 

In our functions.php, we need to add the following code. We want to place this in our setup function just underneath the custom background feature \(line 68\).

```php
//Add theme support for Custom logo
        add_theme_support( 'custom-logo', array(
            'width' => 90,
            'height' => 90,
            'flex-width' => true
        ));
```

Now if we go into our Customizer under Site Settings, there is a new option called Logo. Great our function is working, but now we need to place it somewhere in our theme so that it will show on the front end. 

Lets jump back into our header.php and in our div class "site-branding" we are going to place the following php code which will display our logo on the front end:

```php
<?php the_custom_logo(); ?>
```

And lastly we'll need to add some styling to our custom logo, which will be in header.scss

```css

.custom-logo-link{
    img {
        display: block;
        height: 100px;
        width: auto;
    }
}
```

As its an image it should display as a block, the height will be the same height as the site branding, and width auto for responsive. 

Lastly, I want my site title and tagline to appear next to the logo and in responsive, underneath the logo. How we achieve this is through flexbox. 

We'll need to add an additional class inside site branding so that we can target the correct elements with flexbox. In header.php, just underneath the custom-logo php code, add a div class called "site-branding-text", and close the div just above the closing site-branding div.

```php
<div class="site-branding">
                    
                        <?php the_custom_logo(); ?>
                    <div class="site-branding-text">
                    
			<?php
			if ( is_front_page() && is_home() ) : ?>
				<h1 class="site-title"><a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"><?php bloginfo( 'name' ); ?></a></h1>
			<?php else : ?>
				<p class="site-title"><a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"><?php bloginfo( 'name' ); ?></a></p>
			<?php
			endif;

			$description = get_bloginfo( 'description', 'display' );
			if ( $description || is_customize_preview() ) : ?>
				<p class="site-description"><?php echo $description; /* WPCS: xss ok. */ ?></p>
			<?php
			endif; ?>
                    </div>
		</div><!-- .site-branding -->
```

Always check in your inspector tool to see if the div has been added.

Once you're sure its been added, we need to add a few things to our header.scss file.

```css
.site-branding{
    display: flex;
    min-height: 100px;
}

.custom-logo-link{
    margin-right: 1em;
    img {
        display: block;
        height: 100px;
        width: auto;
    }
}

.site-branding__text{
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100px;
}
```

You need to be always thinking in terms of responsive design, and you would have noticed that the header elements don't exactly do what we want them to do. Take a few moments now to inspector the various elements and add the correct styling to your header.scss to ensure that your responsive header is working correctly. 

