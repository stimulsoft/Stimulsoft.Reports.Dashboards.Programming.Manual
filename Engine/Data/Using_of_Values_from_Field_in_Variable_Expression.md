Using Expression Values in Variable

Besides text, text components can contain expressions. When a component is being rendered, the expression is processed by the report engine, i.e. it is evaluated. The exception is band or page totals: in that case the result is calculated after the band or the whole report has been fully rendered. The order in which components are processed by the report engine core is determined by the hierarchy of the report components. In other words, the higher a component is in this hierarchy, the higher its processing priority when the report is built. The resulting value (the result of evaluating the expression) is passed to the processed (rendered) component.


* **Note**: If a text component with an expression is placed on a band, the rendered report will contain as many instances of the component as there are rows in the band data source.


Sometimes you need to use the result of an expression (the calculated value) in a variable. Consider an example. Suppose there is an expression **{x+y}** placed in the text component **Text10**. To use the result of this expression in a variable, it is not enough to specify the reference **{Text10.Text}**. This is because, in this case, the reference points not to the result of the expression, but to the text expression in the report template. To use the result of the expression in a variable, use one of the following options:


* If you need to get the component value before it is rendered, you should either use the same expression in the variable as in the component, or use two passes, i.e. calculate the value on the first pass and use it in the variable on the second.

* If the value is to be used after the component is rendered, you can use the component's **GetValue** event to get the required value and save (pass) it to the variable.

* You can also, after the whole report has been rendered, iterate over all components of the rendered report in the **EndRender** event and perform the required calculations. Below is a sample script that calculates a page total when the band has the **Can Break** property set and it is not known in advance which page the text component will end up on.


```
foreach (StiPage page in RenderedPages)
            {
                StiText sumComp = null;
                foreach (StiComponent component in page.Components)
                {
                    if (component.Name == "sum_comp")
                    {
                        sumComp = component as StiText;
                        break;
                    }
                }

                double sum = 0;
                foreach (StiComponent comp in page.Components)
                {
                    if (comp.Name == "aaa")
                    {
                        sum += (double)(comp as StiText).TagValue;
                    }
                }
                sumComp.Text = sum.ToString();
            }
```
