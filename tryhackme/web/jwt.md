{%hackmd theme-dark %}
# Authenticate

There are many methods to attack web authentication. 

## Dictionary Attack

* **Tools**: hydra, medusa, burp suite.

## Re-registration

* Register as an existing user with slight modifications e.g. `admin`, register as ` admin` (with a whitespace prefixed).

* Sometimes this will grant privledges of the user.

## JSON Web Token (JWT)

* Cookie generated using HMAC or PKI. Consists of header + payload + signature. 

![](https://i.imgur.com/xI1lc5E.png)


###### tags: `jwt`, `web`, `auth`