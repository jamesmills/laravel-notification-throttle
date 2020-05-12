# Laravel Notification Rate Limit

[![Latest Version on Packagist](https://img.shields.io/packagist/v/jamesmills/laravel-notification-rate-limit.svg?style=flat-square)](https://packagist.org/packages/jamesmills/laravel-notification-rate-limit)
[![Build Status](https://img.shields.io/travis/jamesmills/laravel-notification-rate-limit/master.svg?style=flat-square)](https://travis-ci.org/jamesmills/laravel-notification-rate-limit)
[![Quality Score](https://img.shields.io/scrutinizer/g/jamesmills/laravel-notification-rate-limit.svg?style=flat-square)](https://scrutinizer-ci.com/g/jamesmills/laravel-notification-rate-limit)
[![Total Downloads](https://img.shields.io/packagist/dt/jamesmills/laravel-notification-rate-limit.svg?style=flat-square)](https://packagist.org/packages/jamesmills/laravel-notification-rate-limit)

Rate Limiting Notifications in Laravel using Laravel's native rate limiter to avoid flooding users with duplicate notifications.

## Installation

You can install the package via composer:

```bash
composer require jamesmills/laravel-notification-rate-limit
```

### Update your Notifications
    
Add `ShouldRateLimit` and `RateLimitedNotification` to your the Notifications you would like to Raterate limit.

```php
<?php

namespace App\Notifications;

use Illuminate\Bus\Queueable;
use Illuminate\Notifications\Messages\MailMessage;
use Illuminate\Notifications\Notification;
use Jamesmills\LaravelNotificationRateLimit\RateLimitedNotification;
use Jamesmills\LaravelNotificationRateLimit\ShouldRateLimit;

class NotifyUserOfOrderUpdateNotification extends Notification implements ShouldRateLimit
{
    use Queueable;
    use RateLimitedNotification;

...
```

## Publish Config
    
Everything in this package has opinionated global defaults. However, you can overide everything in the config. 
    
Publish it using the command below.

```
php artisan vendor:publish --provider="Jamesmills\LaravelNotificationRateLimit\LaravelNotificationRateLimitServiceProvider"
```
    
## Options
    
You can custom settings on an individual Notification level.

### Overding the time the notification is rate limited for 

By default an throttled Notification will be throttled for `60` seconds. 
    
Update globally with the `rate_limit_seconds` config setting.

Update for an individual basis by adding the below to the Notification
    
``` php
// Change rate limit to 1 hour
protected $rateLimitForSeconds = 3600;
```
    
### Logging skipped notifciations

By default this package will log all skipped notifications.
    
Update globally with the `log_skipped_notifications` config setting.
    
Update for an individual basis by adding the below to the Notification
    
```php
// Do not log skipped notifications
protected $logSkippedNotifications = false;
```
    
### Skipping uniqueue notifciations

By default the Rate Limiter uses a cache key made up of some opinionated defaults. One of these default keys is a a serialisation of the notification it's using `serialize($notification)`. You may wish to turn this off. 

Update globally with the `should_rate_limit_unique_notifications` config setting.

Update for an individual basis by adding the below to the Notification

```php
// Do not log skipped notifications
protected $shouldRateLimitUniqueNotifications = false;
```


### Testing

``` bash
composer test
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email james@jamesmills.co.uk instead of using the issue tracker.

## Credits

- [James Mills](https://github.com/jamesmills)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

## Laravel Package Boilerplate

This package was generated using the [Laravel Package Boilerplate](https://laravelpackageboilerplate.com).
