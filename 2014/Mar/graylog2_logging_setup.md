#API Logging with Graylog2 - PHP Logging
This is Part 2 of the API Logging with Graylog2 series. [View Part 1](http://xangelo.ca/2014/02/28/api-logging-with-graylog2/)

Now that you have the backend components configured for logging, it's time to set up and configure GELF - the Graylog Extended Log Format.

#### Step 1: Composer
GELF support for PHP is only available via [Composer](https://getcomposer.org). The installation instructures are pretty straight forward, so I won't attempt to go into too much detail - Composer does an excellent job of covering the basics. [Composer Installation Instructions](https://getcomposer.org/download/). 

Once that's done and set up, you'll need to set up your `composer.json` file as follows:

```json
{
    "require": {
        "graylog2/gelf-php": "0.1.*"
    }
}
```

Then just run `composer install` or `composer update` if you already had a composer.json file. 

What this will do is grab the gelf-php libs and toss it into a `./vendor/` directory wherever the `composer.json` file exists. It will also configure an auto-loader so that you don't have to figure out what files to include. 


#### Step 2: Log
Now that we've got the library where we want it, we can go ahead and start the logging!

```php
$transport = new Gelf\Transport\UdpTransport('127.0.0.1');
$publisher = new Gelf\Publisher();
$publisher->addTransport($transport);

$message = new Gelf\Message();
$message->setShortMessage('some log message')
        ->setLevel(6);
                                
$publisher->publish($message);
```

That's all there is to logging to Graylog2. However, there are a lot more things that you can add to your message to give your log a bit more substance.

#### Customizing your message attributes
One of the things that isn't really documented very well (with the library at least) is what exactly can constitute the message. The Message object includes a few additional methods that you can use to get the most out of Graylog2.

- `setShortMessage` - Just a short descriptive message about the log.
- `setFullMessage` - This is where you could include any backtraces or additional dumps.
- `setLevel` - The "severity" of the log. It follows the standard [syslog levels](https://en.wikipedia.org/wiki/Syslog#Severity_levels)
- `setAdditional` - This method accepts two args, the first being a custom key, the second being the value. This is a neat way of adding new information to your log (API keys for example).

---------
Personally, I think Graylog2 is a phenominal way to achieve a proper logging system - something that is often overlooked when you're in "app dev" phase. I've talked about planning when I talked about [Lines of code as a metric](http://xangelo.ca/2014/01/23/lines-of-code/) and logging is definitely one of the most easily overlooked features - that's super easy to add from the beginning. Logging provides you, not just a way to track errors, but also track progress. Imagine tracking your API usage with Graylog2 and watching the requests/hour steadily rise. And then, because you thought about logging from the beginning, you can easily display the additional attribute "api\_key" and "execution\_time" that you've been logging to keep a better eye on your server.
