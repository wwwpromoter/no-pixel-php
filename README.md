# no-pixel-php
Subid pass through redirect using php

## Setup
This method requires no setup, PHP includes all the functionality we need.

## Implementation
For this step we need to get the value from the url. In our exmaple we're getting the subid from the url. We're checking if a `subid` is there, then sending the user to the success page along with the `subid`.

```php
<?php
  $newURL = './success.php';

  if(isset($_GET['subid'])) {
    header('Location: '.$newURL.'?subid='.$_GET['subid']);    
  }
?>
```

#### Success
On the success page we then repeat the similar process of getting the value from the url, then curl the conversion with the `subid`.

Firstly lets check if a `subid` exists in the url. If it does, then curl to the conversion endpoint with the `subid`.

```php
<?php
  if(isset($_GET['subid'])) {
    $subid = $_GET['subid'];

    $url = 'https://creative.wwwpromoter.com/conversion?c=29621&a=4132&nopixel=1&ch=' . $subid;
    
    $ch = curl_init($url);
    $reponse = curl_exec($ch);
  
    curl_close($ch);
  }
?>
```