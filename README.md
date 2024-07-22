# How to use this repo

This project is an ideal Python Django project to use with the [AppMap Navie](https://appmap.io/navie/) AI Architect.

You can use this project to ask various questions of AppMap Navie using the `@diagram` command prefix.  
This will generate Mermaid diagrams that you can use within GitHub Issues & Pull Requests, or otherwise share 
with members of your team. 


## Example Diagrams

Example Question
```
@diagram the functional steps involved when a new user registers for the service.
```

```mermaid
sequenceDiagram
    participant User as User
    participant RegistrationForm as "Registration Form"
    participant RegisterUserMixin as "Register User Mixin"
    participant UserModel as "User Model"
    participant EmailService as "Email Service"

    User->>RegistrationForm: Fills registration form
    RegistrationForm->>RegisterUserMixin: Submits form data
    activate RegisterUserMixin
    
    RegisterUserMixin->>UserModel: Save user instance
    activate UserModel
    UserModel-->>RegisterUserMixin: Returns user object
    deactivate UserModel
    
    RegisterUserMixin->>EmailService: Send registration email
    activate EmailService
    EmailService-->>RegisterUserMixin: Confirmation
    deactivate EmailService
    
    RegisterUserMixin-->>RegistrationForm: Returns user object
    deactivate RegisterUserMixin

    RegistrationForm-->>User: Shows success message
```

![Navie Sequence Diagram Image](navie-django-example.png)