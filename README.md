# PHPCompatibilityChecking
This sample project is designed to validate the compatibility of PHP files in your server folder.

## Step 1
As the first step, you'll need to create a project folder.
```
sudo mkdir php_compatibility
cd php_compatibility
```
Then create a `composer.json` file inside your project folder.
```
nano composer.json
```
Then paste the following content:
```
{
  "name": "yourname/php-compat-check",
  "description": "Project to check PHP 8 compatibility",
  "require-dev": {
    "squizlabs/php_codesniffer": "*",
    "dealerdirect/phpcodesniffer-composer-installer": "^0.7.2",
    "phpcompatibility/php-compatibility": "*"
  },
  "config": {
    "platform": {
      "php": "8.0"
    },
    "allow-plugins": {
      "dealerdirect/phpcodesniffer-composer-installer": true
    }
  },
  "minimum-stability": "dev",
  "prefer-stable": true
}
```
