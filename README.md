# :package_description

[![Latest Version on Packagist](https://img.shields.io/packagist/v/osenco/filament-spatie-passkeys.svg?style=flat-square)](https://packagist.org/packages/osenco/filament-spatie-passkeys)
[![GitHub Tests Action Status](https://img.shields.io/github/actions/workflow/status/osenco/filament-spatie-passkeys/run-tests.yml?branch=main&label=tests&style=flat-square)](https://github.com/osenco/filament-spatie-passkeys/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/actions/workflow/status/osenco/filament-spatie-passkeys/fix-php-code-styling.yml?branch=main&label=code%20style&style=flat-square)](https://github.com/osenco/filament-spatie-passkeys/actions?query=workflow%3A"Fix+PHP+code+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/osenco/filament-spatie-passkeys.svg?style=flat-square)](https://packagist.org/packages/osenco/filament-spatie-passkeys)

<!--delete-->
---
This repo can be used to scaffold a Filament plugin. Follow these steps to get started:

1. Press the "Use this template" button at the top of this repo to create a new repo with the contents of this skeleton.
2. Run "php ./configure.php" to run a script that will replace all placeholders throughout all the files.
3. Make something great!
---
<!--/delete-->

This is where your description should go. Limit it to a paragraph or two. Consider adding a small example.

## Installation

You can install the package via composer:

```bash
composer require osenco/filament-spatie-passkeys
```

You can publish and run the migrations with:

```bash
php artisan vendor:publish --tag="passkeys-migrations"
php artisan migrate
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="filament-spatie-passkeys-config"
```

Under the hood, our package uses simplewebauthn/browser to generate and verify passkeys in your browser. You can install these dependencies via NPM (or Yarn)

```bash
npm install @simplewebauthn/browser
```

Optionally, you can publish the views using

```bash
php artisan vendor:publish --tag="filament-spatie-passkeys-views"
```

This is the contents of the published config file:

```php
return [
     /*
     * After a successful authentication attempt using a passkey
     * we'll redirect to this URL.
     */
    'redirect_to_after_login' => '/dashboard',

    /*
     * These class are responsible for performing core tasks regarding passkeys.
     * You can customize them by creating a class that extends the default, and
     * by specifying your custom class name here.
     */
    'actions' => [
        'generate_passkey_register_options' => Spatie\LaravelPasskeys\Actions\GeneratePasskeyRegisterOptionsAction::class,
        'store_passkey' => Spatie\LaravelPasskeys\Actions\StorePasskeyAction::class,
        'generate_passkey_authentication_options' => \Spatie\LaravelPasskeys\Actions\GeneratePasskeyAuthenticationOptionsAction::class,
        'find_passkey' => Spatie\LaravelPasskeys\Actions\FindPasskeyToAuthenticateAction::class,
    ],

    /*
     * These properties will be used to generate the passkey.
     */
    'relying_party' => [
        'name' => config('app.name'),
        'id' => parse_url(config('app.url'), PHP_URL_HOST),
        'icon' => null,
    ],

    /*
     * The models used by the package.
     * 
     * You can override this by specifying your own models
     */
    'models' => [
        'passkey' => Spatie\LaravelPasskeys\Models\Passkey::class,
        'authenticatable' => env('AUTH_MODEL', App\Models\User::class),
    ],
];
```

## Usage

### Add the package's interface and trait to your user model
```php
You must let your user model (or any model you use to authenticate) implement the HasPasskeys interface and use the InteractsWithPasskeys trait.

namespace App\Models;

use Spatie\LaravelPasskeys\Models\Concerns\HasPasskeys;
use Spatie\LaravelPasskeys\Models\Concerns\InteractsWithPasskeys;
// ...

class User extends Authenticatable implements HasPasskeys
{
    use HasFactory, Notifiable, InteractsWithPasskeys;

    // ... 
}
```

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [:author_name](https://github.com/:author_username)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
