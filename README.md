# DeepSeek PHP Client

[![GitHub Tag](https://img.shields.io/github/v/tag/dependencies-packagist/deepseek-php-client)](https://github.com/dependencies-packagist/deepseek-php-client/tags)
[![Total Downloads](https://img.shields.io/packagist/dt/deepseek/deepseek-php-client?style=flat-square)](https://packagist.org/packages/deepseek/deepseek-php-client)
[![Packagist Version](https://img.shields.io/packagist/v/deepseek/deepseek-php-client)](https://packagist.org/packages/deepseek/deepseek-php-client)
[![Packagist PHP Version Support](https://img.shields.io/packagist/php-v/deepseek/deepseek-php-client)](https://github.com/dependencies-packagist/deepseek-php-client)
[![Packagist License](https://img.shields.io/github/license/dependencies-packagist/deepseek-php-client)](https://github.com/dependencies-packagist/deepseek-php-client)

<p align="center">
  <a href="https://github.com/dependencies-packagist/deepseek-php-client" target="_blank">
    <img src="./docs/deepseek_screenshot.png?raw=true" alt="DeepSeek Usage">
  </a>
</p>

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
    - [Basic Usage](#basic-usage)
    - [Advanced Configuration](#advanced-configuration)
    - [Use with Symfony HttpClient](#use-with-symfony-httpclient)
    - [Get Models List](#get-models-list)
- [Testing](#testing)
- [License](#license)

---

## Features

- **Seamless API Integration**: PHP-first interface for DeepSeek's AI capabilities.
- **Fluent Builder Pattern**: Chainable methods for intuitive request building.
- **Enterprise Ready**: PSR-18 compliant HTTP client integration.
- **Model Flexibility**: Support for multiple DeepSeek models (Coder, Chat, etc.).
- **Streaming Ready**: Built-in support for real-time response handling.
- **Many Http Clients**: easy to use `Guzzle http client` (default) , or `symfony http client`.
- **Framework Friendly**: Laravel & Symfony packages available.

---

## Installation

You can install the package via [Composer](https://getcomposer.org/):

```bash
composer require deepseek/deepseek-php-client
```

Requirements:

> Requires [PHP 8.1+](https://php.net/releases/)

---

## Quick Start

### Basic Usage

Get started with just two lines of code:

```php
use DeepSeek\DeepSeekClient;

$response = DeepSeekClient::build('your-api-key')
    ->query('Explain quantum computing in simple terms')
    ->run();

echo $response;
```

Defaults used:

- Model: `deepseek-chat`
- Temperature: 0.8

### Advanced Configuration

```php
use DeepSeek\DeepSeekClient;
use DeepSeek\Enums\Models;

$client = DeepSeekClient::build(apiKey:'your-api-key', baseUrl:'https://api.deepseek.com/v3', timeout:30, clientType:'guzzle');

$response = $client
    ->withModel(Models::CODER->value)
    ->withStream()
    ->withTemperature(1.2)
    ->run();

echo 'API Response:'.$response;
```

### Use with Symfony HttpClient

the package already built with `symfony Http client`, if you need to use package with `symfony` Http Client , it is easy to achieve that, just pass `clientType:'symfony'` with `build` function.

ex with symfony:

```php
//  with defaults baseUrl and timeout
$client = DeepSeekClient::build('your-api-key', clientType:'symfony')
// with customization
$client = DeepSeekClient::build(apiKey:'your-api-key', baseUrl:'https://api.deepseek.com/v3', timeout:30, clientType:'symfony');

$client->query('Explain quantum computing in simple terms')
       ->run();
```

### Get Models List

```php
use DeepSeek\DeepSeekClient;

$response = DeepSeekClient::build('your-api-key')
    ->getModelsList()
    ->run();

echo $response; // {"object":"list","data":[{"id":"deepseek-chat","object":"model","owned_by":"deepseek"},{"id":"deepseek-reasoner","object":"model","owned_by":"deepseek"}]}
```

---

## Testing

```bash
./vendor/bin/pest
```

Test coverage coming in v2.1.

---

## License

Nacosvel Contracts is made available under the MIT License (MIT). Please see [License File](LICENSE) for more information.
