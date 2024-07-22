# How to use this repo

This project is a fork of the [Django Oscar](https://github.com/django-oscar/django-oscar) project. You can view the original [README here](OLD_README.rst). This an ideal Python Django project to use with the [AppMap Navie](https://appmap.io/navie/) AI Architect.

You can use this project to ask various questions of AppMap Navie using the `@diagram` command prefix.  
This will generate Mermaid diagrams that you can use within GitHub Issues & Pull Requests, or otherwise share 
with members of your team. 


## Example Diagrams
- [Sequence Diagram](#sequence-diagram)
- [Entity Relationship](#entity-relationship)
- [Flow Chart](#flow-chart)
- [Class Map](#class-map)


### Sequence Diagram
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

![Navie Sequence Diagram Image](navie-sequence-diagram-example.png)


### Entity Relationship

```
@diagram the entity relationships between products and other important data objects.  
```


```mermaid
erDiagram
  PRODUCT {
    int id
    string title
    string upc
    text description
  }
  
  PRODUCTCLASS {
    int id
    string name
    string slug
  }
  
  PRODUCTATTRIBUTE {
    int id
    string name
    string code
    string required
    string type
  }
  
  PRODUCTCATEGORY {
    int id
    int product_id
    int category_id
  }
  
  CATEGORY {
    int id
    string name
    string slug
  }
  
  PRODUCTIMAGE {
    int id
    string original
    string caption
    int product_id
  }

  PRODUCTRECOMMENDATION {
    int id
    int primary_id
    int recommendation_id
  }
  
  PRODUCT ||--o{ PRODUCTCLASS : "belongs to"
  PRODUCT ||--o{ PRODUCTATTRIBUTE : "has"
  PRODUCT ||--o{ PRODUCTCATEGORY : "belongs to"
  PRODUCT ||--o{ PRODUCTIMAGE : "has"
  PRODUCT ||--o{ PRODUCTRECOMMENDATION : "has"

  CATEGORY ||--o{ PRODUCTCATEGORY : "includes"
```

![Navie Entitiy Relationship](navie-entity-relationship-example.png)

### Flow Chart

```
@diagram using a flow chart how product sales tax is calculated
```

```mermaid
flowchart TD
    A["Basket"] --> B["BaseCharge.calculate"]
    B --> C{"Has Discount?"}
    C -->|No| D["Calculate excl_tax and incl_tax from BaseCharge"]
    C -->|Yes| E["Apply Discount: Offer.shipping_discount"]
    E --> F["Calculate excl_tax and incl_tax after discount"]
    D --> G["Check if incl_tax is 0"]
    F --> G
    G -->|Yes| H["Return zero excl_tax"]
    G -->|No| I["Calculate excl_tax proportionally"]
    I --> J["Return prices.Price object with updated excl_tax and incl_tax"]
    H --> J
```
![Navie Flow Chart](navie-flow-chart.png)


### Class Map
```
@diagram create a detailed class map of the users, stores, products and other associated classes used
```

```mermaid
classDiagram
  direction LR

  class User {
      +id: int
      +username: str
      +email: str
      +password: str
      +date_joined: datetime
      +last_login: datetime
  }

  class Store {
      +id: int
      +name: str
      +address: str
      +phone: str
  }

  class Product {
      +id: int
      +name: str
      +description: str
      +price: Decimal
      +stock: int
  }

  class Order {
      +id: int
      +user: User
      +store: Store
      +order_date: datetime
  }

  class OrderItem {
      +id: int
      +order: Order
      +product: Product
      +quantity: int
      +price: Decimal
  }

  class Wishlist {
      +id: int
      +user: User
      +name: str
      +created_at: datetime
  }

  class WishlistItem {
      +id: int
      +wishlist: Wishlist
      +product: Product
      +added_at: datetime
  }

  class Review {
      +id: int
      +product: Product
      +user: User
      +rating: int
      +comment: str
      +created_at: datetime
  }

  User --> Order
  Order --> Store
  Order --> OrderItem
  OrderItem --> Product
  
  User --> Wishlist
  Wishlist --> WishlistItem
  WishlistItem --> Product
  
  Product --> Review
  User --> Review
```

![Navie Class Map](navie-class-map.png)