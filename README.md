CodeIgniter-Postal
===========================

This library allows you to fast retrieve informational "flash" messages stored inside `$_SESSION['postal']`. Unlike the usual flash session data, this library will clear the messages only after they are retrieved. This way you can retrieve them at any time, remaining available even after one or more redirects, as long as the $_SESSION is not emptied!

Usage
-----

To install the library, place it inside your libraries folder and load it using
```php
$this->load->library('postal');
```
You can also establish personalized containers for your messages by creating or uploading the postal.php file inside the config directory. The basic content of the postal.php looks like this:
```php
<?php  if ( ! defined('BASEPATH')) exit('No direct script access allowed');
$config['message_types'] = array(
    'success' => array('<div class="success">', '</div>'),
    'error' => array('<div class="error">', '</div>'),
    'message' => array('<div class="message">', '</div>'));
```
In the configuration file you can insert any type of messages, 'success','error' and 'message' being only the default ones.

### Adding messages

Once you've added the library (and, maybe, configured it), you can add messages to a specific message group using:
```php 
$this->postal->add("An error has occurred", "error");
$this->postal->add("The page was updated", "success");
$this->postal->add("How are you?", "message");
```

### Displaying messages

The added messages stays available until you retrieve them, no matter how many controllers you visited. So if you would add them in a specific controller and then redirect, the messages would still be available.

You can retrieve all messages by writing any of the lines below:
```php
echo $this->postal->get(); // THIS WILL RETURN ALL THE MESSAGES AS A STRING

echo $this->postal->get('error'); // THIS WILL ONLY RETURN THE MESSAGES FROM A SPECIFIC GROUP OF MESSAGES

echo $this->postal->get(array('succes','error')); // THIS WILL ONLY RETURN THE MESSAGES FROM SPECIFIED GROUPS

$messages = $this->postal->get(NULL, TRUE); // THIS WILL RETURN ALL MESSAGES AS AN ARRAY, WITHOUT ANY MESSAGE DELIMITERS

$messages = $this->postal->get('error', TRUE); // THIS WILL ONLY RETURN THE MESSAGES FROM A SPECIFIC GROUP OF MESSAGES, WITHOUT ANY MESSAGE DELIMITERS

$messages = $this->postal->get(array('succes','error'), TRUE); // THIS WILL ONLY RETURN THE MESSAGES FROM SPECIFIED GROUPS, WITHOUT ANY MESSAGE DELIMITERS
```

If you want to know how many messages are stored you can use:
```php
$errors = $this->postal->count('error');

$all = $this->postal->count();
```

The stored messages are cleared when you retrieve them using the `get()` method. You can at any time manually clear the messages by using the `clear()` method:
```php
$this->postal->clear();
$this->postal->clear('error');
```
