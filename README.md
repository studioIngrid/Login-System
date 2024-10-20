# Login System

This code is taken from [phptutorial.net](https://www.phptutorial.net/).

On this repository the code is just compiled to one structure.\
Also there is fixed some flaws. 

This application shows how to build a simple PHP login system:
- Registration – show you how to build a account registration form.
- Login – learn how to create a login form.
- Email verification – add the email verification feature when users register for new accounts.
- Remember me – enhance the login form by adding a remember me checkbox to save the login even after closing the web browser.

This system uses a MySQL database.
```
CREATE DATABASE auth;
```

```
CREATE TABLE users
(
    id                int auto_increment PRIMARY KEY,
    username          varchar(25)  NOT NULL,
    email             varchar(255) NOT NULL,
    password          varchar(255) NOT NULL,
    is_admin          tinyint(1)   NOT NULL DEFAULT 0,
    active            tinyint(1)            DEFAULT 0,
    activation_code   varchar(255) NOT NULL,
    activation_expiry datetime     NOT NULL,
    activated_at      datetime              DEFAULT NULL,
    created_at        timestamp    NOT NULL DEFAULT current_timestamp(),
    updated_at        datetime              DEFAULT current_timestamp() ON UPDATE current_timestamp()

);
```

```
CREATE TABLE user_tokens
(
    id               INT AUTO_INCREMENT PRIMARY KEY,
    selector         VARCHAR(255) NOT NULL,
    hashed_validator VARCHAR(255) NOT NULL,
    user_id          INT      NOT NULL,
    expiry           DATETIME NOT NULL,
    CONSTRAINT fk_user_id
        FOREIGN KEY (user_id)
            REFERENCES users (id) ON DELETE CASCADE
);
```


