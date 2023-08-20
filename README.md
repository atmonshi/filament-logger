# Activity logger for filament

[![Latest Version on Packagist](https://img.shields.io/packagist/v/z3d0x/filament-logger.svg?style=for-the-badge)](https://packagist.org/packages/z3d0x/filament-logger)
[![Total Downloads](https://img.shields.io/packagist/dt/z3d0x/filament-logger.svg?style=for-the-badge)](https://packagist.org/packages/z3d0x/filament-logger)

<p align="center">
  <img alt="logger banner" src="https://raw.githubusercontent.com/z3d0x/filament-logger/main/art/banner.jpeg" />
</p>

Configurable activity logger for filament.
Powered by `spatie/laravel-activitylog`

## Features
You can choose what you want to log and how to log it.
- Log Filament Resource Events
- Log Login Event
- Log Notification Events
- Log Model Events
- Easily extendable to log custom events

Note: By default this package will log Filament Resource Events, Access(Login) Events, and Notification Events. If you want to log a model that is not a FilamentResource you will have to manually register in the config file.

## Installation

| Plugin Version | Filament Version |
|----------------|------------------|
| < 0.5.x        | ^2.11            |
| >= 0.6.0       | 3.x              |

This package uses [spatie/laravel-activitylog](https://spatie.be/docs/laravel-activitylog), instructions for its setup can be found [here](https://spatie.be/docs/laravel-activitylog/v4/installation-and-setup)

You can install the package via composer:

```bash
composer require z3d0x/filament-logger
```
After that run the install command:

```bash
php artisan filament-logger:install
```
This will publish the config & migrations from `spatie/laravel-activitylog`

For Filament v3, you need to register a resource in PanelProvider
```php
public function panel(Panel $panel): Panel
{
    return $panel
        ->resources([
            config('filament-logger.activity_resource')
        ]);
}
```
## Authorization
To enforce policies on `ActivityResource`, after generating a policy, you would need to register `Spatie\Activitylog\Models\Activity` to use that policy in the AuthServiceProvider.
```php
<?php
 
namespace App\Providers;
 
use App\Policies\ActivityPolicy;
use Illuminate\Foundation\Support\Providers\AuthServiceProvider as ServiceProvider;
use Spatie\Activitylog\Models\Activity;
 
class AuthServiceProvider extends ServiceProvider
{
    protected $policies = [
        // Update `Activity::class` with the one defined in `config/activitylog.php`
        Activity::class => ActivityPolicy::class,
    ];
    //...
}
```
> If you are using [Shield](https://filamentphp.com/plugins/shield) just register the ActivityPolicy generated by it

## Activity Model resolution
The main `Activity` class being used by the Filament Resource instance will be resolved by Spatie's service provider, which loads the model defined by the configuration key found at `activitylog.activity_model` in `config/activitylog.php`.

## Screenshots
<img alt="logger-index" src="https://raw.githubusercontent.com/z3d0x/filament-logger/main/art/list-screenshot.png">
<img alt="logger-detail-1" src="https://raw.githubusercontent.com/z3d0x/filament-logger/main/art/view-screenshot-1.png">
<img alt="logger-detail-2" src="https://raw.githubusercontent.com/z3d0x/filament-logger/main/art/view-screenshot-2.png">


## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](https://github.com/spatie/.github/blob/main/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Ziyaan Hassan](https://github.com/Z3d0X)
- [Spatie Activitylog Contributors](https://github.com/spatie/laravel-activitylog#credits) 
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
