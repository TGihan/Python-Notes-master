# Python-Notes

# Python latest versions have dll missing issues
  use Python 3.4.2 it works fine

# When you want to run existing python project. Use below step

1. Create virtual environment using 


   virtualenv env

2. Install dependencies

   pip install -r requirements.txt

# If you can't create super user user below
  winpty python manage.py createsuperuser

# How to access python localhost:8000 from android device
  connect both devices via wifi network
  1. You should start server by using
     python manage.py runserver yourip:port
     
     python manage.py runserver 192.160.0.103:8000
     
  2. Check access from your laptop web browser if it is work fine ok
  3. Turn off your <b>windows firwall</b> and <b>anti virus firewalls</b> (important !!)
  4. Enter that ipaddress and port in mobile browser. it works!!
  
#How to host your application on pythonanywhere

Reference link : https://help.pythonanywhere.com/pages/DeployExistingDjangoProject/

1. Create free account
2. Create git repository and upload your application to github
3. Go to pythonanywhere account and click console section
4. Open bash console and clone your repository
   
   <b>git clone "your_git_reository_link"</b>
   
5. If your cloning success you can see your repository in files section
6. Again type <b>mkvirtualenv --python=/usr/bin/python3.4 mysite-virtualenv</b> to create virtualenv for your application
7. If it is success you can see your virtualenv in files section .virtualenv folder (Not your project folder. It create in base folder)
8. Fine, Now we want to create sample webapp for our project. In order to do that goto web section and click add a new webapp
9. Choose manualcreate > python 3.4 and next
10. Edit souce code path to your cloned repoditory location eg: /home/TharinduGihan/python-demo/
11. Virtualenv location to your project virtualenv location eg: /home/TharinduGihan/.virtualenvs/pythondemo-virtualenv
12. Then goto your project folder via bash console which has your requirements.txt file (cd yourproject)
13. Then type <b>pip install -r requirements.txt</b>
14. Edit wsgi.py file in web section. Delete all content and copy and paste below code and change required points as your project
```
# +++++++++++ DJANGO +++++++++++
# To use your own django app use code like this:
import os
import sys
#
## assuming your django settings file is at '/home/TharinduGihan/mysite/mysite/settings.py'
## and your manage.py is is at '/home/TharinduGihan/mysite/manage.py'
#path = '/home/TharinduGihan/mysite'
path = '/home/TharinduGihan/python-demo/src'

if path not in sys.path:
    sys.path.append(path)

os.environ['DJANGO_SETTINGS_MODULE'] = 'blog.settings'
#
## then, for django >=1.5:
from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
## or, for older django <=1.4
#import django.core.handlers.wsgi
#application = django.core.handlers.wsgi.WSGIHandler()
```
*Configure MySQL database*

15. create mysql database and set password in database section
16. Change your setting.py according to pythonanywhere mysql details
17. Type again <b>pip install mysqlclient</b> in your bash to install mysqlclient lib
18. Goto folder which has manage.py file via bash and execute below commands
    
    <b>python manage.py makemigration</b>
    
    <b>python manage.py migrate</b>
    
19. Goto virtualenv console from web section
    
    <b>python manage.py createsuperuser</b>
    
20. Ok.. Its done goto your app url

#How to download your code as a zip file from pythonanywhere
open bash console from file tab and execute below command

zip -r myzipfile my_folder_name

# Django reset password with shell

You may try through console:

`python manage.py shell`

then use following script in shell

`from django.contrib.auth.models import User
User.objects.filter(is_superuser=True)`

will list you all super users on the system. if you recognize yur username from the list:


`usr = User.objects.get(username='your username')
usr.set_password('raw password')
usr.save()`

and you set a new password (:

#How to backup your mysql database
`mysqldump -u TharinduGihan -h TharinduGihan.mysql.pythonanywhere-services.com 'TharinduGihan$dbname'  > db-backup.sql`
