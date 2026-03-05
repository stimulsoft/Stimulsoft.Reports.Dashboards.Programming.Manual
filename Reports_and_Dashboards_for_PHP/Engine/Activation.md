# License Activation

After purchasing the product, you should activate license for used components. There are several ways of license key connection.

### Activation using code string

To activate from a code string, simply copy the encrypted license text from  [your personal account](https://devs.stimulsoft.com/) on the website and register it using the static function `setPrimaryKey()`, which is located in the `StiLicense` class:


**index.php**

```php

<?php
    use Stimulsoft\StiLicense;

    StiLicense::setPrimaryKey('Your activation code...');
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/How%20to%20Activate%20the%20Product.php).

### Activation using a file

To activate using a license file, download the `license.key` file from  [your personal account](https://devs.stimulsoft.com/) on the website, copy it into your PHP project folder, and register it using the static function `setPrimaryFile()`, located in the `StiLicense` class:


**index.php**

```php

<?php
    use Stimulsoft\StiLicense;

    StiLicense::setPrimaryFile('license.key');
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/How%20to%20Activate%20the%20Product.php).

### Activation of the report generator only

In some cases, you may need to activate the report generator separately from other components. In this case, the `license` key can be registered using the `setKey()` or `setFile()` method of the license property of the report object:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;

    $report = new StiReport();
    $report->license->setKey('Your activation code...');
    $report->license->setFile('license.key');
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/How%20to%20Activate%20the%20Product.php).


**Protection against license key theft**

If the license is activated using a code string, it can be added conditionally. For example, you may want to add the license key only for registered users:


**index.php**

```php

<?php
    use Stimulsoft\StiLicense;
    if (!empty($sessionID))
        StiLicense::setPrimaryFile('Your activation code...');
?>
```

Also, we recommend you change the location and name of the license key file, for example:


**license.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->license->setFile('private/a15fc0ef64e6.key');
?>
```

### Activation of a license in a single file

If the application components are used across multiple separate files, such as a report generator, viewer, and designer, it is more convenient to apply the license in a single file instead of activating each component separately. To achieve this, you need to create a dedicated file where the license will be applied, and in all other files containing components, simply include the prepared license file using the standard `require_once` statement.


**license.php**

```php

<?php
    use Stimulsoft\StiLicense;
    
    StiLicense::setPrimaryKey('Your activation code...');
?>
```


**license.php**

```php

<?php
    require_once 'license.php';
    
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    
    ...
?>
```
