# Printing Report from Code

The report generator provides the ability to print a report from code. You can use the `print()` method of the report object for this purpose. Here's an example of invoking the print dialog for a pre-built report:


**index.php**

```php

<?php
    use Stimulsoft\Report\StiReport;
    
    $report = new StiReport();
    $report->loadFile('reports/SimpleList.mrt');
    $report->render();
    $report->print();
    $report->printHtml();
?>
```

The full example code is available on [GitHub](https://github.com/stimulsoft/Samples-Reports.PHP/blob/master/Working%20with%20Report/Printing%20a%20Report%20from%20Code.php).


> **Information**
>
> Printing a report doesn’t automatically trigger the report generation, so you need to call the `render()` method beforehand to build the report for a loaded report template. For completed documents (already built reports), this method is not necessary.

By default, all pages of the built report will be printed. There’s also an option to specify a particular page or range of pages for printing. You can pass the desired value as a parameter to the `print()` function, which can be a specific page or a range of pages. Here's an example of printing specified pages of the report:


**index.php**

```php
<?php
    $report->print(5);
    $report->print('1,3-8');
?>
```
