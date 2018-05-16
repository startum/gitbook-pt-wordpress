# Conditional Statements

One of the primary reasons for using a programming language like PHP is to write conditional statements.

Conditional statements let you test if a certain condition exists and then execute code that is appropriate for that condition.

```php
<?phpif(statement that must be true){    (code to be executed when the "if" statement is true);}else{    (code to be executed when the "if" statement is not true);}?>
```

The simplest, and most common conditional statement you'll see in WordPress is the if statement, or the if else statement. 

A common use of the statement is to test if any posts are available for a specific page. 

```php
if ( is_home() || is_single() ) {
 
   the_content();
 
}
else {
 
   the_excerpt();
 
}
```

If there are posts available, then you'll write out the code to display those posts, using many of the template tags we looked at previously. 

If there are no posts available we would use the else portion of the conditional statement, and echo out a message saying there are no posts available. 

This simple example will work for checking and displaying a single post. But most of the time in WordPress, we combine conditional statements with loop statements that let us apply our code as many times as necessary.

For example, when you're looping through multiple blog posts on a blog listing page. So let's take a look now at how we would combine a conditional statement with a simple loop.

