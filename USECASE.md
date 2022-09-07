# Use Case

This file contains a list of use cases based on Vtiger Customizer

## Customize the "Login Process"

Into Vtiger the login process is based on the 'doLogin' method placed here <https://code.vtiger.com/vtiger/vtigercrm/blob/master/modules/Users/Users.php#L338>.

Now I need to check if user is present on a Custom Source (eg. a public list of Footbal Arbiter/Referee).

```php
<?php
Vtiger_Customizer::extendMethod('Users::doLogin', function($self, $args) {

  // Do the standard 'doLogin' methods
  $success = $self->doLogin($args['password']);

  // If user exists on DB and login is correct, now I check if exists on public list of Footbal Arbiters 
  if ($success) {
    $listOfArbiters = json_decode(file_get_contents('<public-url-of-footbal-data>'), true);
    
    $success = in_array($self->user, $listOfArbiters);
  }

  return $success;
});
```

## Customize the every "Emails Body"

Into Vtiger all email sent pass from this function 'send_mail' placed here <https://code.vtiger.com/vtiger/vtigercrm/blob/master/modules/Emails/mail.php>.

Now I need to append to all emails I send the message "This email is property of VTIGER do not touch please!"

```php
<?php
Vtiger_Customizer::extendFunctions('send_mail', function($args) {

  $args['contents'] .= "\n\n" . "This email is property of VTIGER do not touch please!"; 
  
  return send_mail($args);
});


