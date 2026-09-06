# Secure Cloud Architecture Plan

Users
  ↓
CDN
  ↓
Load Balancer
  ↓
Application Servers
  ↓
Private Database

Users

Users access the application through a web browser or other client. Their requests are sent through the cloud infrastructure to access the application's services and data.

CDN

The CDN stores cached copies of static content, such as images, CSS files, and JavaScript files, closer to users. This improves loading speed and reduces the amount of traffic sent to the application servers.

Load Balancer

The load balancer distributes incoming requests across multiple application servers. This helps prevent one server from becoming overloaded and improves the availability and reliability of the application.

Application Servers

Application servers process requests from users and run the application's backend logic. Multiple application servers can be used to handle large amounts of traffic. These servers should be placed in a private subnet to reduce direct exposure to the Internet.

Private Database

The database stores important application data, such as student records and user information. The database should remain private and should not be directly accessible from the Internet. Only the application servers should be allowed to communicate with the database.

# Public and Private Resources

CDN — Public

The CDN must be public since users access it via the Internet; it is used for delivering static content including images, CSS files, JavaScript files, videos, and other website resources. The website loads more quickly and the application servers have to do less work when the CDN stores copies of these files near the users. However, even though the CDN is public it should still make use of security measures like HTTPS in order to protect the connection between the users and the website.

Load Balancer — Public

The load balancer must be public since it needs to accept requests from users via the Internet; it functions as a point midway between the users and the application servers. Upon users accessing the application, the load balancer spreads out their requests among the various application servers. This stops any one server from getting an excessive amount of traffic and helps ensure that the application remains available even when a large number of users are accessing it at the same time.

Application Server — Private

The application servers must remain private since they house the principal backend logic of the application and should not be accessible directly from the Internet. Users send their requests to the public load balancer, which then passes on the requests to the application servers. Placing the application servers in a private subnet gives an extra level of security and decreases the likelihood of unauthorized access. The servers are still able to communicate with the database and other necessary services via controlled network connections.

Database — Private

The database must remain private since it contains important application information, for example student records, user accounts and other data. It should not be accessible directly from the Internet since this could increase the chances of unauthorized access or data theft. Communication with the database should be permitted only for the application servers. Access can be restricted to trusted application servers by placing the database in a private subnet and making use of security rules or firewalls.


# Security Controls
IAM

Access to the cloud environment should be restricted to authorized users; administrators should have full access, whereas teachers and staff should have access only to the resources they need for their jobs. Students should have limited access to the information that belongs to them.

MFA

MFA should be turned on for administrators, teachers, staff, and for any other accounts with access to sensitive student information, since it adds an extra security layer in the event that a password is compromised.

Firewall / Security Group

The firewall or security groups should only allow necessary connections:

Internet → Load Balancer = Allowed
Load Balancer → Application Server = Allowed
Application Server → Database = Allowed
Internet → Database = Blocked

The database must not be accessible directly from the Internet.

Encryption

Student information must be encrypted in order to guard against unauthorized individuals being able to read the names, grades, contact details, and other records since the data might be intercepted or accessed without permission.

Logging

The system must record significant activities such as user logins, failed login attempts, changes to student records, administrator actions, database access, and security-related events; logs enable one to determine who carried out an action and when it took place.

Monitoring

The system must keep an eye on suspicious activities including repeated failed login attempts, logins from unusual locations, attempts at unauthorized access, unexpected modifications to student records, and odd network traffic.

Backup

The database must have routine backups in order to avoid permanent data loss resulting from accidental deletion, system failures, cyberattacks, or other unforeseen issues. This way, the student information can be restored when needed.


# Principle of Least Privilege

# Shared Responsibility Model

Responsibility	Cloud Provider or Customer?
Physical data center	Cloud Provider
Physical servers	Cloud Provider
User accounts	Customer
Student data	Customer
IAM permissions	Customer
Application security	Customer
Database access rules	Customer
Backups	Customer

What is meant by the security of the cloud?
The security of the cloud involves protecting the cloud infrastructure itself, the cloud provider being responsible for securing the physical data centres, the servers, the networking equipment, and the underlying infrastructure. The cloud provider ensures that physical servers are safeguarded against unauthorized physical access.

What is meant by Security in the Cloud?
Security in the cloud involves protecting the data, applications, and resources which the customer places in the cloud, and the customer is responsible for areas such as user accounts, permissions, application security, data, and database access.



1. What resource can be accessed directly from the Internet?

The load balancer must be accessible directly from the Internet since it needs to receive requests from users and forward them to the application servers.

2. There is a reason why the database should stay private.

It is necessary that the database should stay private in order to prevent sensitive student information from being accessed without authorization or from internet attacks.

3. There is a reason why users should not connect directly to the database.

Users must not connect directly to the database since doing so could lead to sensitive data being exposed and security risks being created. Instead, they should access the data via the application server.

4. What is the reason for using a load balancer?

A load balancer spreads the incoming requests from users among several application servers, which in turn helps to improve both performance and availability.

5. What will occur if one application server fails?

The load balancer has the capability of forwarding the requests to the other application servers that are functioning properly, which enables the system to keep on operating.

6. Why is a CDN used?

A content delivery network serves static content like images, CSS, JavaScript, and videos by using servers that are nearer to the users. This in turn makes the website load more quickly.

7. There is a good reason why administrator accounts should use multi-factor authentication.

Administrator accounts should use multi-factor authentication since they have high-level access, and it offers an extra security layer if the administrator's password is stolen.

8. There should be no reason to give administrator access to every employee.

Administrator access should be restricted since employees only need access to the resources they need for their jobs, and restricting access helps to reduce the risk of accidental or unauthorized changes.

9. Why are logging and monitoring important?

Logging is used to record important system activities, while monitoring serves to detect suspicious behaviour. Together, these measures aid in identifying and responding to security issues.

10. Why are backups important?

It is important to have backups since they enable the database and the student information to be restored following an accidental deletion, a system failure, a cyberattack, or a loss of data.

