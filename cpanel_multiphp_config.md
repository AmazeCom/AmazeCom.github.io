cPanel EA4 MultiPHP under CloudLinux
====================================

Using cPanel EA4 MultiPHP on a CloudLinux system with the CL PHP Selector has a
number of interactions to be aware of.

There are two major decisions to make regarding which PHP a domain should run under:

- The first is whether to use the cPanel EA4 compiled versions of PHP (`ea-phpXX`)
  or the CloudLinux compiled versions (`alt-phpXX`).
- The second is which handler to use:  `dso` (apache module), `cgi`, `suphp`, or `php-fpm`.

Each version of PHP installed on the server has a system wide selection between
`dso`, `cgi`, and `suphp`. &nbsp; There can never be more than one version selected as
`dso` and if one is chosen it has to be one of the cPanel EA4 versions (`ea-phpXX`). &nbsp;
[Amaze](https://www.amaze.com.au/) defaults to using `suphp` for all versions of PHP.

Each domain can be individually configured to use a specific version of PHP and to
either use `php-fpm` or not. &nbsp; If it is not configured to use `php-fpm` then the PHP
will be run using the system wide selected handler for that version of php (for
[Amaze](https://www.amaze.com.au/) that usually means `suphp`). &nbsp; Like with `dso` only
the cPanel EA4 versions (`ea-phpXX`) are allowed to run under `php-fpm`.

There are currently
([cPanel version 68](https://documentation.cpanel.net/pages/viewpage.action?pageId=2449480))
a number of bugs and caveats to be aware of:

- Only the superuser can change whether a domain is using `php-fpm` or not. &nbsp; If you wish
  to change this for a particular domain on an [Amaze](https://www.amaze.com.au/) hosted cPanel
  please sumbit a support ticket (either at [support.amaze.com.au](https://support.amaze.com.au/)
  or by emailing [support@amaze.com.au](mailto:support@amaze.com.au))
- The [MultiPHP Manager for cPanel](https://documentation.cpanel.net/display/68Docs/MultiPHP+Manager+for+cPanel)
  does not prevent you from choosing a CloudLinux PHP version (`alt-phpXX`) even when `php-fpm`
  is enabled. &nbsp; If you do choose one then all apache will start throwing `503 Service Unavailable`
  errors.
