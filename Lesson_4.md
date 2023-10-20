## HTML Templating With JavaScript:

Handlebars uses string replacement that allows you to write the names of properties of your objects within handlebars and have them replaced with the property values.
 - With Handlebars templates, you have property names surrounded by two opening and closing curly brackets

A handlebars conditional is `false` if the property value is `false`, `undefined`, `null`, `0`, or an empty string

The `#` sign tells handlebars to perform an action at that point before rendering
```HTML
<li>
  <h3>{{name}}</h3>
  <dl>
    <dt>Quantity:</dt>
    <dd>{{quantity}}</dd>
    <dt>Price:</dt>
    <dd>
      ${{price}}
      {{#if on_sale}}
      <strong>SALE!</strong>
      {{/if}}
    </dd>
  </dl>
</li>
```

This is known as an `if` helper. There are other built in helpers in handlebars and they all start with `#` and end with a closing element

In order to use this to output our items, we would use template pre-compilation to create and store a function that can be called to build our template based on an object passed into it.
The handlebars library gives us an object named `Handlebars` that holds the methods we will need to create templates and partials. To create a template function, we would use the `compile` method to
provide it an HTML string that we want to use as our template. 

We can create a template in our HTML using a script element
```HTML
<script id='productTemplate' type='text/x-handlebars'>
  <li>
    <h3>{{name}}</h3>
    <dl>
      <dt>Quantity:</dt>
      <dd>{{quantity}}</dd>
      <dt>Price:</dt>
      <dd>
        ${{price}}
        {{#if on_sale}}
        <strong>SALE!</strong>
        {{/if}}
      </dd>
    </dl>
  </li>
</script>
```
Here, we give it a `type` of `text/x-handlebars`.

Then, in JS we can use the `Handlebars.compile` method to convert HTML into a template function 
```JS
let productTemplate = Handlebars.compile($('#productTemplate').html());
```
Here we have read the contents of the script elements using JQuery's `.html` method and passed that into the `Handlebars.compile` method. We get a function in return that can be
passed in an object, and the function will return an HTML string with all the properties filled in. We can now loop over the products array and write the template using the item 

```JS
let $list = $('ul');
let productsHtml = products.map(function(product) {
  return productTemplate(product);
});

$list.html(productsHtml.join(''));
```




