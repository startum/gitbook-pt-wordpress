# Simple Loops

The most simple loop we find in WordPress is the WHILE loop. This loop says repeat the same bit of code as long as a given condition is true.

```php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>

	<h2><?php the_title() ;?></h2>
	<?php the_post_thumbnail(); ?>
	<?php the_excerpt(); ?>

<?php endwhile; else: ?>

	<p>Sorry, no posts to list</p>

<?php endif; ?>
```

Lines 1, 7, and 11 are the basic logic that separate the code for when there are blog posts and no blog posts. Lines 3, 4, 5 do the actual work of displaying the title, featured image, and excerpt.

In line 1, the part of code that reads while \( have\_posts\(\) \) : the\_post\(\); is what programs the process of repeating for as many times as there are posts.

_Note:_ Using pagination on a site is a way of limiting the number of posts that are looped through on a page. After the loop reaches the default number of posts to display \(set under Settings &gt; Reading &gt; Blog pages show at most\) it will show how many more pages are available. 

Here is what a simple loop looks like for displaying a title and the main content for a page.

```php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>

	<h1><?php the_title() ;?></h1>	
	<?php the_content(); ?>

<?php endwhile; else: ?>

	<p>Sorry, this page does not exist</p>

<?php endif; ?>
```

All of this is still very theoretical and may not make complete sense yet. 

Let's take a look now at some actual code in a WordPress theme to see this conditional statement and WHILE loop combine together in what we call in WordPress, the loop.

