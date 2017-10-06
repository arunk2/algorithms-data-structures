## Problem:
Cookies are not being set for 'amazonaws.com' and sub-domains after upgrading to chrome 57 or 58. Earlier it used to work fine.

## How to reproduce: 
Following is a test file in one of the EC2 instance, which sets a cookie in browser for domain '.amazonaws.com'. 
But, the cookie is never set. (Note: we access the EC2 public DNS which is a host in amazonaws.com)

    <?php
    $cookie_name = "user";
    $cookie_value = "John Doe";
    setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/",     ".amazonaws.com"); // 86400 = 1 day
    ?>
    <html>
    <body>

    <?php
    if(!isset($_COOKIE[$cookie_name])) {
        echo "Cookie named '" . $cookie_name . "' is not set!";
    } else {
        echo "Cookie '" . $cookie_name . "' is set!<br>";
        echo "Value is: " . $_COOKIE[$cookie_name];
    }
    ?>
    
** But when we set the cookie with our domain '.company.com', and accessed via our subdomain DNS. Cookie are being set there. **

> This behaviour of cookie not being set happened only after upgrading to chrome 57 or 58.

## Root cause: 
Chrome is working as expected, because the 'elb', 'compute' subdomains of '.amazonaws.com' are added to the **'Public Suffix List'** recently. 
I guess it went live in chrome 56+ (56.0.2924.87) and hence subsequent version behaves differently.

Any domains in 'Public Suffix List' will be ignored by browser to set cookies. 
As, it consider those to be not owned by any individual and cookies are not set in browser.
