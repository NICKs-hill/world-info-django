# simple-django-project
## Installation
- I update the readme file for installation and running the project because the main repository is very old and no more details about installation and running the project.
- I update aslo ```world/models.py``` file, because main file have a ```Tab space``` issues.
- I run this project on AWS EC2 Instance ```Ubuntu Server 22.04 LTS``` OS Image. so, I my case I follow below requirements.

### Prerequisites

#### 1. Install Python
Install ```python-3.7```

```
# add repository
sudo apt update
sudo add-apt-repository ppa:deadsnakes/ppa

# install python 
sudo apt install python3.7
python3.7 --version
```
#### 2. Install pip  
Install pip ```python3-pip```

```
sudo apt install python3-pip
pip --version
```

#### 3. Install MySQL and other dependency
Install ```mysql-8``` & dependency
```
sudo apt install mysql-server python3.7-distutils python3.7-dev libmysqlclient-dev
```

#### 4. Setup virtual environment
```
# Install virtual environment
sudo pip install virtualenv

# Make a directory
mkdir envs

# Find location of python3.7
which python3.7

# Create virtual environment
virtualenv -p /usr/bin/python3.7 ./envs

# Activate virtual environment
source envs/bin/activate
```

#### 5. Clone git repository
```
git clone https://github.com/bjnandi/simple-django-project.git
```

#### 6. Install project requirements
```
cd simple-django-project/
pip install -r requirements.txt
```

#### 7. Create User & Load sample data into MySQL
```
# Open mysql bash
sudo mysql -u root -p

# Create user, set password & given permission
create user 'django'@'localhost' identified by 'password123';
grant usage on *.* to 'django'@'localhost';
grant all privileges on world.* to 'django'@'localhost';

# Give the absolute path of the file
source /home/ubuntu/simple-django-project/world.sql
exit;
```

#### 8. Edit project settings
Here I put demo database information for testing purpose and I use [https://mailtrap.io/](https://mailtrap.io/) for get OTP in email. You can follow [https://help.mailtrap.io/article/109-getting-started-with-mailtrap-email-testing](https://help.mailtrap.io/article/109-getting-started-with-mailtrap-email-testing) for getting ```Credentials``` & test email to get OTP.
```
# Open settings file
nano panorbit/settings.py

# Open Host (Add you host public IP address)
ALLOWED_HOSTS = ["c9ae666b.ngrok.io","35.173.130.201", "localhost"]

# Edit Database configurations with your MySQL configurations.
# Search for DATABASES section.
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'world',
        'USER': 'django',
        'PASSWORD': 'password123,
        'HOST': 'localhost',
        'PORT': '3306',
    }
}

# Edit email configurations.
# Search for email configurations
EMAIL_USE_TLS = True
EMAIL_HOST = 'sandbox.smtp.mailtrap.io'
EMAIL_HOST_USER = '<Username>'
EMAIL_HOST_PASSWORD = '<Password>'
EMAIL_PORT = 587

# save the file
```
#### 9. Run the server
```
# Make migrations
python manage.py makemigrations
python manage.py migrate

# For search feature we need to index certain tables to the haystack. For that run below command.
python manage.py rebuild_index

# Run the server
python manage.py runserver 0:8001

# your server is up on port 8001
```

```

