# NNTP

Client for communicating with servers throught the Network News Transfer Protocol (NNTP) protocol.

[![Latest Stable Version](https://poser.pugx.org/rvdv/nntp/v/stable)](https://packagist.org/packages/rvdv/nntp)
[![Build Status](https://travis-ci.org/robinvdvleuten/php-nntp.svg?branch=master)](https://travis-ci.org/robinvdvleuten/php-nntp)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/robinvdvleuten/php-nntp/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/robinvdvleuten/php-nntp/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/robinvdvleuten/php-nntp/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/robinvdvleuten/php-nntp/?branch=master)
[![StyleCI](https://styleci.io/repos/14465626/shield?branch=master)](https://styleci.io/repos/14465626)

## Installation

The recommended way to install the library is [through composer](http://getcomposer.org).

```bash
composer require thibaultjunin/nntp:^0.9.0
```

## NNTP?

> NNTP specifies a protocol for the distribution, inquiry, retrieval,
> and posting of news articles using a reliable stream (such as TCP)
> server-client model. NNTP is designed so that news articles need only
> be stored on one (presumably central) host, and subscribers on other
> hosts attached to the LAN may read news articles using stream
> connections to the news host.

> -- RFC Abstract ([source](http://tools.ietf.org/html/rfc977))

## Usage

Here is an example that fetches 100 articles from the _php.doc_ of the _news.php.net_ server:

```php
<?php

use Rvdv\Nntp\Connection\Connection;
use Rvdv\Nntp\Client;

$connection = new Connection('news.php.net', 119);
$client = new Client($connection);

$client->connect();

$overviewFormat = $client->overviewFormat();
$group = $client->group('php.doc');
$articles = $client->xover($group['first'], $group['first'] + 100, $overviewFormat);

// Process the articles further...

$client->disconnect();
```

## Tests

To run the test suite, you need install the dependencies via composer, then run PHPUnit.

```bash
$ composer install
$ php vendor/bin/phpunit
```

## License

MIT © [Robin van der Vleuten](https://www.robinvdvleuten.nl)
