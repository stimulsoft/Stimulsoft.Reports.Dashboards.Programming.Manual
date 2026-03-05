# Adding Custom Functions

When integrating the report designer into a custom application, you can add your own JavaScript functions to the data dictionary of the report designer. Once added, these functions can be used when creating reports and dashboards. Below is an example of adding a function to calculate a sum total:


**designer.php**


<?php

use Stimulsoft\Designer\StiDesigner;

use Stimulsoft\Enums\Types;

use Stimulsoft\Report\StiFunctions;

StiFunctions::addFunction("MyCategory", "MySum", "MySum", "MySum", "", Types::string,"Return Description", [Types::int], ["value"], ["Descriptions"],"myFunc");

$designer = new StiDesigner();$designer->printHtml();
?>


...


<script>

function myFunc (value) {

if (!Stimulsoft.Data.Extensions.ListExt.isList(value))
return Stimulsoft.Base.Helpers.StiValueHelper.tryToNumber(value);

return Stimulsoft.Data.Functions.Funcs

.skipNulls(Stimulsoft.Data.Extensions.ListExt.toList(value))

.tryCastToNumber()

.sum();
};
</script>

If you are using the designer without an HTML template, you can pass the function code instead of its name. The other parameters of the function will remain the same:


**designer.php**


<?php

use Stimulsoft\Designer\StiDesigner;

use Stimulsoft\Enums\Types;

use Stimulsoft\Report\StiFunctions;

StiFunctions::addFunction("MyCategory", "MySum", "MySum", "MySum", "", Types::string,"Return Description", [Types::int], ["value"], ["Descriptions"],
"

function myFunc (value) {

if (!Stimulsoft.Data.Extensions.ListExt.isList(value))

return Stimulsoft.Base.Helpers.StiValueHelper.tryToNumber(value);


return Stimulsoft.Data.Functions.Funcs

.skipNulls(Stimulsoft.Data.Extensions.ListExt.toList(value))

.tryCastToNumber()

.sum();

};

");

$designer = new StiDesigner();$designer->printHtml();
?>
