# PHPCompatibilityChecking
This sample project is designed to validate the compatibility of PHP files in your server folder.

## Requirements
- PHP 5.4+
- Composer

PHP_CodeSniffer requires PHP version 5.4.0 or greater Since this project was created through `Composer`, you should [install Composer](https://getcomposer.org/) before starting this.


## 🗂 Step 1 - Create Project
As the first step, you'll need to create a project folder.
```bash
sudo mkdir php_compatibility
cd php_compatibility
```

## 📝 Step 2 - Create `composer.json` manually
Then create a `composer.json` file inside your project folder.
```bash
nano composer.json
```
Then paste the following content:
```json
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
## 📥 Step 3 - Install Dependencies
Run this in the same folder:
```bash
composer install
```
This will
- Install PHP_CodeSniffer (Linter that checks PHP code style and compatibility)
- Install PHPCompatibility (A set of rules for checking PHP version compatibility)
- Install PHPCSUtils and required plugins
- Register the PHPCompatibility standard automatically
## ✅ Step 4 - Run PHP 8 Compatibility Check
Run this in the same folder
```bash
./vendor/bin/phpcs --standard=PHPCompatibility --runtime-set testVersion 8.0 /path/to/your/php/files
```
### Output of Compatibility Check
Once you've set everything up and run the compatibility check, the **output** of `phpcs` will list **errors and warnings** in your PHP code that are **not compatible with PHP 8.0**.
```vbnet
FILE: /var/www/html/myapp/test.php
-----------------------------------------------------------------------------------------------------
FOUND 2 ERRORS AND 1 WARNING AFFECTING 3 LINES
-----------------------------------------------------------------------------------------------------
  12 | ERROR   | Function each() is deprecated since PHP 7.2 and removed in PHP 8.0
  25 | WARNING | The create_function() function is deprecated since PHP 7.2 and removed in PHP 8.0
  40 | ERROR   | The implode() function's parameter order changed in PHP 7.4
-----------------------------------------------------------------------------------------------------
```
🔍 What the Output Tells You
- Line number: Where the issue occurs
- Type: ERROR (incompatible with PHP 8) or WARNING (may cause issues)
- Message: What’s wrong and which PHP version introduced the change
### Customize the output
- Show only errors (suppress warnings):
```bash
./vendor/bin/phpcs --standard=PHPCompatibility --runtime-set testVersion=8.0 -n /path
```
- Output in summary format:
```bash
./vendor/bin/phpcs -s --standard=PHPCompatibility --runtime-set testVersion=8.0 /path
```
- Save output to a report:
```bash
./vendor/bin/phpcs --standard=PHPCompatibility --report=full > report.txt
```
- exclude certain folders. You can use wildcards (*) in folder names:
```bash
./vendor/bin/phpcs
--standard=PHPCompatibility
--runtime-set testVersion=8.0
--ignore=/path/to/ignore1/*,/path/to/ignore2/*
/path/to/scan
```
- If you're in your project root and want to ignore, for example, the vendor/ and tests/ folders:
```bash
./vendor/bin/phpcs --standard=PHPCompatibility --runtime-set testVersion=8.0 --ignore=vendor/*,tests/* ./
```
🧪 **Example:**
You have 70 folders inside /home/user/web/, and each of them contains a subfolder named data/, which you want to exclude from the PHP 8 compatibility scan.
```bash
./vendor/bin/phpcs \
  --standard=PHPCompatibility \
  --runtime-set testVersion=8.0 \
  --ignore=*/data/* \
  /home/gayan/web/
```
🔍 **Explanation:**
- `--ignore=*/data/*` matches any path ending with `/data/`, no matter how deep it is.
- It effectively skips:
  - `/home/user/web/project1/data/`
  - `/home/user/web/project2/data/`
  - ...
  - `/home/user/web/project70/data/`
- Exclude multiple patterns (example)
```bash
--ignore=*/data/*,*/cache/*,*/tmp/*
```
- If you just want to verify what would be scanned, add `-s` for a summary or `-v` for verbose mode:
```bash
./vendor/bin/phpcs -s -v
--standard=PHPCompatibility
--runtime-set testVersion=8.0
--ignore=*/data/*
/home/gayan/web/
```

## Reference
* [https://aureatelabs.com/blog/how-to-check-your-code-is-compatible-with-php/](https://aureatelabs.com/blog/how-to-check-your-code-is-compatible-with-php/)
* [https://github.com/PHPCompatibility/PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility)
* [https://github.com/PHPCSStandards/PHP_CodeSniffer/](https://github.com/PHPCSStandards/PHP_CodeSniffer/)

## License
This code is released under the GNU Lesser General Public License (LGPL). For more information, visit [http://www.gnu.org/copyleft/lesser.html](http://www.gnu.org/copyleft/lesser.html)
