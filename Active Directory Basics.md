# Active Directory Basics

> A Windows domain is a group of users and computers under the administration of a given business. The main idea behind a domain is to centralise the administration of common components of a Windows computer network in a single repository called Active Directory (AD). The server that runs the Active Directory services is known as a Domain Controller (DC).

* `Centralised identity management`: All users across the network can be configured from Active Directory with minimum effort.
* `Managing security policies`: You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

## Active Directory (Task 3)

* `Users` - Users are one of the objects known as security principals, meaning that they can be authenticated by the domain and can be assigned privileges over resources like files or printers
* `People`: users will generally represent persons in your organisation that need to access the network, like employees.
* `Services`: you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service.

* 
