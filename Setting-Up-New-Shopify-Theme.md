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
