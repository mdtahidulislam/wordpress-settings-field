# Wordpress Setting Field
```php
/**
 * add settings field
 * init action hook
 * add section settings
 * add section callback
 * add fields settings
 * register fields into option table (save value to db)
 * display fields (get and display value from db)
*/
function textdomain_settings_init(){
    // add section settings
    add_settings_section( 'textdomain_section', __('Section Name', 'textdomain'), 'textdomain_section_callback', 'general', array());

    // add fields settings
    add_settings_field('textdomain_field_id', __('Field Label', 'textdomain'), 'textdomain_display_field', 'general', 'textdomain_section', array());

    // register fields into option table
    register_setting( 'general', 'textdomain_field_id', array('sanitize_callback' => 'esc_attr') );
}

//add section callback
function textdomain_section_callback(){
    echo "<p>".__('Description for the section', 'textdomain')."</p>";
}

// display fields
function textdomain_display_field(){
    // get initila value
    $option_value = get_option('textdomain_field_id');
    // create field
    printf("<input type='text' name='%s' id='%s' value='%s' />", 'textdomain_field_id', 'textdomain_field_id', $option_value);
}

// init action hook
add_action('admin_init', 'textdomain_settings_init');
```
