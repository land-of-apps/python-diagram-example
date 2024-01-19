
```
python -m venv venv
source venv/bin/activate
python -m pip install --upgrade pip
pip install -e .\[test\]
pip install -r requirements.txt
make sandbox
sandbox/manage.py runserver
```

Prompts:

1a) Where are the the files or functions where user registration happens in my code base? I want to modify the specific places in the code where a new user registration validation occurs in order to add a simple offline captcha for Django.  

1b) Identify in my code base where new user registration occurs.  I plan to modify the specific places in the code where a new user registration occurs in order to update the form and add a simple offline captcha for this project.  

1c) Locate where in my code base new user registration occurs. I plan to update the website form and the relevant backend code where a new user registers and add a simple offline captcha for this project.  

Provide a solution with the least amount of code modification to add an open source Django library that can do a simple math based offline captcha to the the registration form (src/oscar/apps/customer/forms.py), to add a new field and associated validation, and the associated registration view. 

Using the django-simple-math-captcha library, provide a simple example update to the custom registration template to render the captcha field, handle form validation, and display an error if the captcha is incorrect.