# Lithe Mail

A package that simplifies SMTP email sending in PHP applications, providing flexible integration with environment variables for easy configuration.

## Installation

You can install the package via [Composer](https://getcomposer.org/). Run the following command in your terminal:

```bash
composer require lithemod/mail
```

Make sure the environment variable package is properly configured, as `support-mail` relies on these settings.

## Usage

Here’s a comprehensive guide on how to use the package to send emails:

### 1. Setting Up Environment Variables

Create a `.env` file in the root of your project and define your email settings:

```bash
MAIL_HOST=smtp.yourprovider.com
MAIL_PORT=587
MAIL_USERNAME=your-email@domain.com
MAIL_PASSWORD=your-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@domain.com
MAIL_FROM_NAME=Your Name or Company
```

### 2. Sending a Simple Text Email

```php
<?php

require 'vendor/autoload.php';

use Lithe\Support\Mail;
use Lithe\Support\Env;

// Load environment variables
Env::load(__DIR__);

// Send the email
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->send();

if ($mail) {
    echo 'Email sent successfully!';
} else {
    echo 'Failed to send email.';
}
```

### 3. Sending an HTML Email

```php
<?php

$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->subject('Email Subject')
    ->html('<h1>Email body in HTML</h1>')
    ->send();

if ($mail) {
    echo 'Email sent successfully!';
} else {
    echo 'Failed to send email.';
}
```

### 4. Adding CC and BCC Recipients

You can add CC and BCC recipients to your emails using the following methods:

#### Adding CC

```php
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->cc('cc@example.com', 'CC Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->send();
```

#### Adding BCC

```php
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->bcc('bcc@example.com', 'BCC Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->send();
```

### 5. Setting Reply-To Address

You can set a reply-to address using the `replyTo` method:

```php
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->replyTo('replyto@example.com', 'Reply-To Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->send();
```

### 6. Attaching Files

To attach files to your email, use the `attach` method:

```php
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->attach('/path/to/file.txt', 'CustomFilename.txt')
    ->send();
```

### 7. Adding Custom Headers

You can add custom headers to your email as follows:

```php
$mail = Mail::to('recipient@domain.com', 'Recipient Name')
    ->subject('Email Subject')
    ->text('Body of the email in plain text')
    ->addHeader('X-Custom-Header', 'HeaderValue')
    ->send();
```

## Requirements

- PHP 7.4 or higher
- Environment variables configured in the `.env` file

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.