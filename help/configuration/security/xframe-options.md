---
title: X-Frame-Options header
description: Use X-Frame-Options to control page renderings.
---

# X-Frame-Options header

To help prevent [Clickjacking](https://owasp.org/www-community/attacks/Clickjacking) exploits, we added an option to use the [X-Frame-Options](https://datatracker.ietf.org/doc/html/rfc7034) HTTP request header in requests to your storefront.

The `X-Frame-Options` header enables you to specify whether or not a browser should be allowed to render a page in a `<frame>`, `<iframe>`, or `<object>` as follows:

- `DENY`: Page cannot be displayed in a frame.
- `SAMEORIGIN`: (default) Page can be displayed only in a frame on the same origin as the page itself.

>[!WARNING]
>
>The `ALLOW-FROM <uri>` option has been deprecated because Commerce-supported browsers no longer support it. See [Browser compatibility](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#browser_compatibility).

>[!WARNING]
>
>For security reasons, Adobe strongly recommends against running the Commerce storefront in a frame.

## Implement `X-Frame-Options`

Set a value for `X-Frame-Options` in `<magento_root>/app/etc/env.php`. Following is the default value:

```php
'x-frame-options' => 'SAMEORIGIN',
```

>[!TIP]
>
>It is more secure to edit the `env.php` file than it is to set a value in the Admin.

## Verify your setting for `X-Frame-Options`

To verify your setting, view HTTP headers on any storefront page. There are several ways to do this, including using a web browser inspector.

The following example uses curl, which you can run from any machine that can connect to your Commerce server over the HTTP protocol.

Use the following command:

```bash
curl -I -v --location-trusted '<your storefront URL>'
```

Look for the `X-Frame-Options` value in the headers.