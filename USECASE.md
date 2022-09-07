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
  // With this if an Ar
  if ($success) {
    $listOfArbiters = json_decode(file_get_contents('<public-url-of-footbal-data>'), true);
    
    $success = in_array($self->user, $listOfArbiters);
  }

  return $success;
});

