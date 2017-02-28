# Plugin Theme

A list of useful functions.

## Content

Add a text before and after a content or a title. 

```
add_filter('the_content', 'add_content_single');
add_filter('the_title', 'add_title_single');

function add_content_single($content)
{
    if (! is_single()) {
        return $content;
    }
    
    return 'before ' . $content . ' after';
}
```
