# Magento 2 sample module

How to create **Magento 2 Hello World Simple Module** using this module we are display simple "Hello Mage" and also we are learn how create frontend route and how to use route.


## Magento 2 Hello World module

- Step 1: Create the module folder.
- Step 2: Declare module using module.xml
- Step 3: Register module using registration.php file.
- Step 4: Install setup, Enable module.
- Step 5: Check new module is active.
- Step 6: Create route  for module.
- Step 7: Create controller for module.
- Step 8: Check that the module is working.


### Step 1. Create the module folder.

There are two possible locations for modules in Magento 2
- app/code/
- vendor/
The location of module can be describe based on how module has been installed. so here is a question Which of these locations should you choose for your new module?

If you build a module for a specific project to enhance or change functionality, it is best to choose the app/code folder.
If you build an extension, it is better to use composer to create it, and put your module in the vendor/<YOUR_VENDOR>/module-something folder.

So here we will use `Learning` for Vendor name and `HelloMage` for ModuleName. So we need to make this folder:
`app/code/Learning/HelloMage`

### Step 2. Create the etc/module.xml file for declare module.

Create `module.xml` file under `app/code/Learning/HelloMage/etc`.

~~~
app/code/Learning/HelloMage/etc/module.xml
~~~

And the content for this file:

~~~ xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
     <module name="Learning_HelloMage" setup_version="1.0.0" />
</config>
~~~


### Step 3. Create registration.php file for register module.

Create `registration.php` file under `app/code/Learning/HelloMage` Add below content to `registration.php` file.

~~~
app/code/Learning/HelloMage/registration.php
~~~

And it’s content for our module is:

~~~
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Learning_HelloMage',
    __DIR__
);
~~~

### Step 4. Install setup and enable module using command.

We can install the module through command line.

~~~
php bin/magento setup:upgrade
~~~

Below is another usefull command 

~~~
Module status  : php bin/magento module:status
~~~

~~~
Enable module  : PHP bin/magento module:enable Learning_HelloMage
~~~

~~~
Disable module : PHP bin/magento module:disable Learning_HelloMage
~~~


### Step 5. Check new module is active.

To check the new module is enable open file `app/etc/config.php` and find `Learning_HelloMage` check value = 1

### Step 6. Create route  for module.

We need to create route for the controller action.

Create `route.xml` file under `app/code/Learning/HelloMage/etc/frontend/routes.xml` and add below content.

~~~
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="learning" frontName="hellomage">
            <module name="Learning_HelloMage" />
        </route>
    </router>
</config>
~~~

The Router is used to assign a URL to a corresponding controller and action. In this module, we need to create a route for frontend area. So we need to add this file:

### Step 7. Create controller form module.

Create action controller file under `app/code/Learning/HelloMage/Controller/Index/Index.php` and add below code.

~~~ php
<?php
namespace Learning\HelloMage\Controller\Index;
 
class Index extends \Magento\Framework\App\Action\Action
{
  public function __construct(
\Magento\Framework\App\Action\Context $context)
  {
    return parent::__construct($context);
  }
 
  public function execute()
  {
  echo 'Hello Mage'; 
    exit;
  }
}
~~~


### Result : 

Open your browser, enter this link:

~~~
http://example.com/<router_name>/<controller_name>/<action_name>
~~~


If you have followed all above steps, you will see `Hello Mage` when open the url `http://example.com/hellomage/index/index`



