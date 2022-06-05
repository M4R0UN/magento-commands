# Theory
### What are the Liquid Filters
Filters are the methods that modify the output of <br><br>
Strings <br>
Numbers <br>
Variables <br>
Objects <br><br>
They are placed within an output tag `{{}}` and are denoted by a pipe character `|`

### Filters
**asset_url** is a URL that returns the URL of a file inside the assets folder of a theme.<br>
**stylesheet_tag** or **script_tag** is an HTML filter used to create HTML elements based on liquid properties or store assets that you specify. <br>

# Setting up new empty shopify theme with theme kit

### Install Theme Kit
For Linux: <br> 
    `curl -s https://shopify.dev/themekit.py | sudo python`
<br>
Or follow instructions <a href="https://shopify.dev/themes/tools/theme-kit">here</a>.

### Create Development Store
1. Log in into developers.shopify.com
2. Stores > Add Store > Development Store > Fill up the following form

### Create Custom App
1. In your store click Apps > Develop apps > Create an app
2. Select your app > Configuration > Admin API integration > Themes -> Allow read and write themes > Save > Install App

### Create Password using Theme Kit Access
1. Go to Apps > Customize your store > Search for theme kit > Add app > Install app > Create theme Kit password > fill out name and email > Create password
2. Check your email it should give you the password
3. In the command line go to your project folder and run:
    `theme new --password=[password from previous step] --store='mystore.myshopify.com' --name=[name your theme]`
    
###### Dont forget to add gitignore for config.yml


# Setting up Bootstrap
It can be done either through content delivery network or by downloading & uploading the source files to the project. <br><br>
**Steps for uploading:**
1. Go to getbootstrap.com > Download > Compiled CSS and JS Download
2. In css folder (of the file that you just downloaded) copy *bootstrap.min.css* and *bootstrap.min.css.map* and put it into the project **assets** folder
3. In js folder (of the file that you just downloaded) copy *bootstrap.min.js* and *bootstrap.min.js.map* and put it into the project **assets** folder
4. In VS code go to layout/theme.liquid change
```
{{ 'application.css' | asset_url | stylesheet_tag }}
{{ 'application.js' | asset_url | script_tag }}
```
to
```
{{ 'bootstrap.min.css' | asset_url | stylesheet_tag }}
{{ 'bootstrap.min.js' | asset_url | script_tag }}
```
5. Its better practise to move `{{ 'bootstrap.min.js' | asset_url | script_tag }}` before `</body>` tag.

# Development
`{{ content_for_index }}` an object used in the index.liquid. It allows you to customize your homepage dynamically. By using this object , you will have the "Add Section" button which you can find on customizer page. <br>
`schema` tags are used to create settings for your sections and you can find these settings in your customizer page. Schema tags only accepts JSON formatted code. <br>
`{% capture %}{% endcapture %}` Capture is a variable tag used to capture the string inside of the opening and closing tags and assign it to a variable. Variables that you create using capture are stored as strings. <br>
`{% cycle %}` Loops through a group of strings and outputs them in the order that they were passed as parameters. Each time cycle is called, the next string that was passed as a parameter is output.<br>
`selected_or_first_available_variant` is an attribute of products object, used to return the variant object of the selected product<br>
### Paginate Tag
Is used for splitting products, articles, and search results across multiple pages. This will not only make your web pages smaller, but it will also help users to easily navigate from one page to another. 
