# Django settings app

## Installation

pip install ma-settings

### in settings.py file:

1 add 'ma-settings' into INSTALLED_APPS

2 define MASTER_SETTINGS dict with your settings definition

template:

    MASTER_SETTINGS = {
        '(setting_name)':{
            'type' : '(setting_type)',
            'default': (default value), # optional
            'options': (choice options), # optional
            'model': (foreign model), # optional, use only when foreign type is chosen
        }
    }

example:

    MASTER_SETTINGS = {
        'Max email size (kb)': {
            'type': 'integer',
            'default': 400,
        },
        'Text color': {
            'type': 'choices',
            'options': ['White', 'Black', 'Red', 'Blue'],
            'default': 'White',
        },
        'Our rate': {
            'type': 'float',
            'default': 1.0,
        },
        'Email from': {
            'type': 'string'
        },
        'Default client': {
            'type': 'foreign',
            'model': 'my_app.Client'
        }
    }

3 define BASE_SETTINGS_TEMPLATE_NAME

BASE_SETTINGS_TEMPLATE_NAME = "template_name.html"

Template file must contain empty {% block settings %}


### in urls.py add include('ma_settings.urls')

url(r'^settings/', include('ma_settings.urls')),

Use url name 'master_settings_home' to access settings page

### run commands

    python manage.py syncdb
    python manage.py init_settings



## Using

To get setting use

     from ma_settings import master_settings
     master_settings.get('setting name', default='default')

To set new value:

    master_settings.set('setting name', [value|model_instance])

To check if setting exists:

    master_settings.exists('setting name')

After updating settings definition in settings.py run this command to update settings

     python manage.py init_settings

