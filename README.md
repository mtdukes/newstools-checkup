#checkup

An open-source Django app to survey politicians, by the Newsday investigations team. [Read about it here](http://newsday.github.io). Deploy instructions to come.

(NOTE: This project uses [Isotope](http://isotope.metafizzy.co/), which may require a purchasing a [license](http://isotope.metafizzy.co/docs/license.html) in some cases.)

##Setup instructions (local)
Follow these instructions to set up checkup on your local machine for testing (installation for Amazon EC2 coming soon).

1. Clone the repo.
   ```bash
   $ git clone https://github.com/mtdukes/newstools-checkup.git
   ```
   
2. Install [Django](https://docs.djangoproject.com/en/1.7/intro/install/). To do that in a [virtual environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/):
   ```bash
   $ mkvirtualenv venv
   $ pip install Django
   ```

3. Outside your ```newstools-checkup``` directory, start a new Django project to store your checkup application.
   ```bash
   $ django-admin.py startproject mycheckup
   ```

4. Navigate to your Djano project directory and make a copy of the contents of the ```newstools-checkup``` directory.
   ```bash
   $ cd mycheckup
   $ cp -R ../newstools-checkup/* ./
   ```

5. Run the setup file inside your project directory.
   ```bash
   $ python setup.py install
   ```
6. Using the ```local_settings.example``` file included with the checkup app, edit the ```settings.py``` file located in your project subfolder. To run properly, the settings file needs the following items copied from ```local_settings.example```:
   * ```ROOT_PATH```
   * ```STATIC_ROOT```
   * ```BUILD_DIR```
   * ```SITE_ID```
   * ```INSTALLED_APPS``` 
   * ```GRAPPELLI_INDEX_DASHBOARD```
   * ```GRAPPELLI_ADMIN_TITLE```
   * ```BAKERY_VIEWS```
   * ```BITLY_OAUTH2```
   * All email-related items
   * ```POLITICAL_PARTIES```
   * ```TEMPLATE_BASE```
   
   In addition, edit ```TIME_ZONE``` to your local time zone
7. Tell Django to create database tables.
   ```bash
   $ python manage.py migrate
   ```
8. [Create a Django superuser](https://docs.djangoproject.com/en/1.7/intro/tutorial02/) for initial login and follow the prompts.
   ```bash
   $ python manage.py createsuperuser
   ```
9. In ```urls.py``` in your project directory (NOTE: *not* the ```checkup``` directory), change the url patterns variable to the following:
   ```python
   urlpatterns = patterns('',
       (r'^grappelli/', include('grappelli.urls')),
       url(r'^checkup/', include('checkup.urls')),
       url(r'^admin/', include(admin.site.urls)),
   )
   ```
10. Run local server to begin setting up checkup.
   ```bash
   $ python manage.py runserver
   ```