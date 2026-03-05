# Printing a Report From Code

The reporting tool allows you to print a report from code. To achieve this, you can utilize the special `print()` method on the report object.


**app.py**

```python

report = StiReport()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))
report.render()
report.print()
```


**Information**


Printing a report does not cause it to be automatically built, so for a loaded report template, you must first call the `render()` method, which will build the report. For finished documents (built reports), this method is not required.

By default, all pages of the generated report will be printed. It is possible to specify a page or range of pages to print. To achieve this, simply pass the required value as a parameter to the `print()` function. For example:


**app.py**

```python

report = StiReport()
report.loadFile(url_for('static', filename='reports/SimpleList.mrt'))

report.render()
report.print(5)
report.print('1,3-8')
```
