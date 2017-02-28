# Wordpress - Useful Methods

## Filter text

```
$name = sanitize_text_field($_POST['name']);
$name = esc_html($_POST['name']);
$name = esc_sql($_POST['name']);
```

