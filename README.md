Hi everyone,

thank you for your interest for this plugin.

Unfortunately, I am running out of time these days, so I won't update it.

If anyone has a solution to make it better, please feel free to fork it.

Maybe, I'll come back in a few months, but right now I have a big project that will take all my energies.


plg_mvcoverride
===============

Joomla plugin to override Joomla MVC.

Plugin used (and updated for j!3) in these joomla docs :

 [How to override the component mvc from the Joomla! core - Joomla! Documentation](http://docs.joomla.org/How_to_override_the_component_mvc_from_the_Joomla!_core) 

The joomla 2.5.x version is here :

Plugin Override - Joomla! Extensions Directory

http://extensions.joomla.org/extensions/style-a-design/templating/15611

### Usage example 
For a component :
>/templates/yourtemplate/code/com_search/views/search/view.html.php

For a module :
>/templates/yourtemplate/code/module_name/helper.php 


### Issue
No more issue ATM.

Alex Chartier found a working solution.

If someone finds an issue, please tell us.

# Joomla 4 Usage

Copy the file you want to override into your template folder, in the ```code``` directory.  Follow the same directory structure from the directory in the component folder.  For example, if you want to override a method in RegistrataionModel from the com_users component, copy the file from ```components/com_users/src/Model/RegistrationModel.php``` to ```templates/yourtemplate/code/com_users/src/Model/RegistrationModel.php```.

* Change the class that the overriding class extends to the name of the class plus "Default".
* Add the core files namespace, adding the "*Default" class name.

```php
namespace Joomla\Component\Users\Site\Model;

\defined('_JEXEC') or die;

use Joomla\CMS\Application\ApplicationHelper;
use Joomla\CMS\Component\ComponentHelper;
use Joomla\CMS\Date\Date;
use Joomla\CMS\Factory;
use Joomla\CMS\Form\Form;
use Joomla\CMS\Form\FormFactoryInterface;
use Joomla\CMS\Language\Multilanguage;
use Joomla\CMS\Language\Text;
use Joomla\CMS\Log\Log;
use Joomla\CMS\Mail\MailTemplate;
use Joomla\CMS\MVC\Factory\MVCFactoryInterface;
use Joomla\CMS\MVC\Model\FormModel;
use Joomla\CMS\Plugin\PluginHelper;
use Joomla\CMS\Router\Route;
use Joomla\CMS\String\PunycodeHelper;
use Joomla\CMS\Uri\Uri;
use Joomla\CMS\User\User;
use Joomla\CMS\User\UserHelper;
use Joomla\Database\ParameterType;

/**
 * Registration model class for Users.
 *
 * @since  1.6
 */
class RegistrationModel extends FormModel
{
    ...
```

changes to:

```php
namespace Joomla\Component\Users\Site\Model;

\defined('_JEXEC') or die;

use Joomla\CMS\Application\ApplicationHelper;
use Joomla\CMS\Component\ComponentHelper;
use Joomla\CMS\Date\Date;
use Joomla\CMS\Factory;
use Joomla\CMS\Form\Form;
use Joomla\CMS\Form\FormFactoryInterface;
use Joomla\CMS\Language\Multilanguage;
use Joomla\CMS\Language\Text;
use Joomla\CMS\Log\Log;
use Joomla\CMS\Mail\MailTemplate;
use Joomla\CMS\MVC\Factory\MVCFactoryInterface;
use Joomla\CMS\MVC\Model\FormModel;
use Joomla\CMS\Plugin\PluginHelper;
use Joomla\CMS\Router\Route;
use Joomla\CMS\String\PunycodeHelper;
use Joomla\CMS\Uri\Uri;
use Joomla\CMS\User\User;
use Joomla\CMS\User\UserHelper;
use Joomla\Database\ParameterType;
use Joomla\Component\Users\Site\Model\UsersModelRegistrationDefault;

/**
 * Registration model class for Users.
 *
 * @since  1.6
 */
class RegistrationModel extends UsersModelRegistrationDefault
{
    ...
```

You can remove any methods from the overriding file that don't have code changes in them, as they are automatically inherited from the original class that you're extending.

The MVC Override plugin supports core Jooml component Controllers, Models, and Views.


# Development build

Build uses Phing to package plugin into an installer.

## Install Phing

To install Phing globally, use Composer and run from the cmd line:

```
composer global require phing/phing
```

## Build packages for install

Run from the cmd line in the project directory:

```
phing
```

Installer is output to the ```dist``` directory.
