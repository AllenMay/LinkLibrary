Application Security: OWASP Top 10 Curriculum

TLS

HTTP Public Key Pinning
HPKP

Salt is a random value added to the content before hashing

SHA256/SHA512

Adaptive Algorithms
- bcrypt
- PBKDF2

Q. What is the purpose of public key pinning?
A. To prevent man-in-the-middle attacks over TLS connections. 

The correct answer is to prevent man-in-the-middle attacks over TLS connections. Public key pinning allows the web application to "pin" the certificates that will be used in a TLS connection, preventing an attacker from impersonating the real server through the use of a fraudulently signed certificate.

Q. What is the purpose of an authentication process?
A. To prove that a user is who they claims to be. 

The correct answer is to prove that a user is who they claim to be. User authentication processes are intended to verify that a user is who he or she claims to be, uniquely distinguishing that individual from all other users of a system.

Q. Which of the following are adaptive password storage algorithms?
A. PBKDF2 and Bcrypt

The correct answer is PBKDF2 and Bcrypt. These adaptive password storage algorithms have been specifically designed to be very computationally intensive, there by making the recovery of passwords very difficult.

Q. Which of the following are ways that developers inadvertently reveal user credential information?
A. Login failure, password reset, user creation, and lockout messages 

The correct answer is login failure, password reset, user creation and lockout messages. For example, developers may inadvertently reveal user credential information, such as the username or email address, through various error messages that the application displays.

Q. Which of the following are good practice methods for storing user passwords?
A. Multiple rounds of hashing with a random salt or adaptive algorithms.

The correct answer is multiple rounds of hashing with a random salt or adaptive algorithms. The best practice for the storage of passwords in a web application is to use many hundreds to thousands of rounds of hashing, coupled with a random salt or the use of an adaptive algorithm that has been designed for the secure storage of password hashes.

=====================================================


Enforce access controls

Session Management

Session Token
Generate a unique token

Session tracking becomes the foundation of acces control
TLS (Transport layer security)

Serve entire website over TLS 

Downgrade attack 

HTTP Strict Transport Security
Used to Leverage HSTS

Session Tracking Mechanisms

-URL Rewriting
  URL ID will be embeded in the web itself

-Basic Authentication
  Strongly recomend basic authentication not be used


-Cookies
  "Secure" says the cookie should only use TLS

Sesion cloning vs. session hijacking





Session fixation attacks




Q. Why is session management a particular concern in web applications?
A. HTTP is stateless. 

The correct answer is that HTTP is stateless. The concept of a session is not unique to web applications, but the fact that the underlying protocol (HTTP) is stateless makes it of particular concern when developing web applications.


Q. How are session tokens typically used in web applications?
A. To reauthenticate the user and perform authorization activities. 

The correct answer is to reauthenticate the user and perform authorization activities.

Q. Which of the following is a best practice for session tokens?
A. Session tokens must be sent over a secure channel. 

The correct answer is that session tokens must be sent over a secure channel. If we fail to do this, anyone who can view the network data can impersonate the user by reusing the session token.



# Sensitive Data Exposure: Insecure Cryptographic Storage

HASH-512

Hash + cryptographic salt

key expansion techniques & random data
PRNG - psudo random number generator

OpenSSL  
GNU-TLS  
Java Cryptographic Architecture  
Bouncy Castle  
.Net Cryptography Framework  

Key expansion  


- bcrypt  
- PBKDF2  


Symmetric Encryption  
When the data is decrypted, the key is used  

Asymetric Encryption
Public Key Cryptography


Insecure Cryptographic Storage
- Unencrypted Confidential Information  
- Poor 

Two Key Risks  
- Unauthorized Access by Privleged Users  
- Sensitive Data Exposure  


Q. How can proper encryption controls defend our data at rest?
! By providing strong authentication controls to reinforce the algorithms used to store the data in the database.


Q. What is the problem with using statistical random number generators?
A. Statistical random number generators do not generate cryptographically secure random values. 

The correct answer is that statistical random number generators do not generate cryptographically secure random values. The reason is that the values produced are generated from a statistical method rather than using true random sources, which is required for cryptographic methods.

Q. What value does asymmetric encryption add when storing sensitive data?
A. If asymmetric encryption methods are used, even if the attacker retrieves the public key, the data will remain secure.

The correct answer is that using an asymmetric method will enable the data to remain secure. Even if the attacker manages to compromise the systems in the path between the application and the database, if the method is properly implemented, only the public key is accessible. This key cannot be used to decrypt the data.

Q. What risk exists when symmetric encryption is used to store sensitive data in the database?
A. The decryption key must be in the data path and is likely accessible to administrators and attackers.

The correct answer is that the decryption key must be in the data path and is likely accessible to administrators and attackers. If a symmetric algorithm is used, the encryption key must be in the path between the application and the database, which is a significant risk. This means that administrators and potential attackers can either access the key or leverage the encryption/decryption system to access the cleartext data.




# OWA A3 Sensitive Data Exposure: Insufficient Transport Layer Protection

## Sensitive Data Exposure  
Insufficient Transport Layer Protection


HSTS Header
HTTP Strict Transport Security 

Certificate Pinning  
- Uses Public-Key-Pins


Q. Why should TLS be used to send the user authentication form to the user?
If it isn't, the user might worry that their credentials will not be handled securely.
If TLS isn't used when the form is presented to the user, it cannot be used for submission.
!TLS requires that all API calls enforce certificate pinning and use HSTS for requests.


Q. Which of the following is an effective way to enforce the use of TLS for users connecting to your application?
A. Require the Strict-Transport-Security header

The correct answer is that the Strict-Transport-Security header is used to enforce a TLS requirement on web application connections.

Q. Why must TLS be used during and after the user authentication occurs?
A. After authentication, the session token is used to reauthenticate the user; the token must also be protected.

The correct answer is that after authentication, the session token is used as a surrogate for the user credentials in all subsequent requests. The token must be sent over a secure channel or impersonation of the user becomes trivial.

Q. What causes Mixed Content warnings?
A. When parts of the content referenced by the HTML specify "http" rather than "https".

The correct answer is that mixed content, or mixed frames, issues occur when a portion of a web page sent over TLS specifies an absolute URL to a page element using HTTP (without TLS).

Q. Why must TLS be used during user authentication requests?
A. TLS will ensure that the user credentials are encrypted on the network.

The correct answer is that TLS provides encryption in transit, preventing the user credentials from being exposed.

## OWA A4 XML External Entity (XXE)

Recent edition to the OWASP 10 top



Soap 1.2
SAML 


Q. What is a straightforward way to avoid XXE issues?
A. Use something other than XML to serialize/deserialize your data objects

The correct answer is to use something other than XML to serialize/deserialize your data objects. If we serialize the data with something else, such as JSON, we can safely send this serialized data as an XML blob without any concern that an XML library will improperly execute any XXE contained within it.

Q. What is the primary way that XML External Entities are leveraged against an application?
A. When the XML input from the attacker causes the libraries to access an external file or URL.

The correct answer is that XXE is exploited is by leveraging a flaw in a library that will process XML containing a file or URL for some external content, automatically loading or processing that external data.


Q. Which of the following is a strong indicator that you may have XXE vulnerabilities?
A. If your systems are using anything older than SOAP 1.2

The correct answer is that if you are using a SOAP implementation older than SOAP 1.2, it is very likely that you have systems with potential XXE vulnerabilities.

# OWA A5 Broken Access Control

## Authentication & Authorization  
Direct Object References  

## Mandatory Access Control  
## Principle of Complete Mediation  
## Indirect Object Reference

"Use and automated process that ..."


OWA A5 Broken Access Control - Quiz [1/3]

Q. What is a common characteristic of broken access control?
A. Users can read or modify data that they should not be able to access.

The correct answer is that users can read or modify data that they should not be able to access.

Q. Which of the following is a good strategy to reduce the number of broken access control issues?
A. Ensure that authorization checks are performed as close to the data as possible.
!Ensure that all requests and responses are transmitted over TLS with HMAC.
!Ensure that strong user credentials are in use with required periodic changes.

The correct answer and best approach is to put authorization checks as close to the data as possible. If this is done consistently and enforced in the backend, it dramatically reduces the potential for a flaw elsewhere in the application that would allow a user to view data that he or she should not be able to view.


Q. Which of these is an example of a direct object reference?
A. The URL contains a parameter with the value of an ID in a database, which is used to retrieve data from the server.
!The backend API allows users to send requests at it directly, directly accessing the server objects.
!The user's password is used to uniquely identify the user, creating a direct object reference to the user object.

The correct answer is the URL contains a parameter with the value of an ID in a database. A direct object reference is typically a database ID that is sent in a request from the front end and which is used in a database query to retrieve an object. Modifying the requested ID will frequently allow users to view arbitrary records in the database.

# OWA A6 Security Misconfiguration

Information Security 

Ensure the development and test environments mirror the production environment with throughouh testing of configuration settings.

Q. Which of the following would count as a "Security Misconfiguration" for the purposes of this OWASP issue?
!Using dynamic SQL statements with user input in the application.
!Configuring the browser to cache cookies locally on the client.
A. Default and test accounts and credentials within the application.

The correct answer is that configuration issues include both the configuration of the underlying server/services and configuration within the application itself, such as leaving test and other default accounts enabled within the deployed application.

Q. Why should default features in web application development frameworks be disabled if they are not actively being used and managed?
A. Default APIs and serializers can lead to inadvertent exposures where security controls are not applied.
!Default interfaces create consumer confidence issues when the logos are inadvertently displayed.
!Default API endpoints can be easily leveraged to discover administrative credentials on the server.

The correct answer is that leaving default features, including automatic APIs and serializers, enabled can quickly lead to points through which data can be accessed where no application layer security controls are being applied. They effectively allow an attacker to bypass the application and interact with the data layer directly through the exposed automatic API.

Q. Which of the following best describes the relationship between the Development, Test, and Production environments?
!The Development environment is managed by developers, while the Test and Production environments are not.
!The Development and Test environments are configured less securely than the Production environment.
A. The Development, Test, and Production environments should be configured identically.

To provide the most robust security while simultaneously assuring that the application will function properly in production (an availability and integrity issue), the Development, Test, and Production environments should be configured identically, which is the correct answer.


# OWA A7 Cross-Site Scripting (XSS)

- Web Services
- Databases
- End users

## Malicious Activities
- Stealing session cookies
- Logging keystrokes
- Conducting intranet port scanning
- Rewriting the contents of the web page
- Conducting phishing attacks
- Instaling malicious software

Tools:

- OWASP Cheat Sheet Series
https://cheatsheetseries.owasp.org/

- Browser Exploitation Framework
  - BeEF
  https://beefproject.com/

- XSS Prevention Cheat Sheet
  - https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.md

3 flavors:
## Stored or persistent XSS
## Reflext XSS
## DOM-based XSS


Encode ALL output.


HTTPOnly flag - set on Cookies  
X-XSS Protection Header  
Content Security Policy  


OWA A7 Cross-Site Scripting (XSS) - Quiz [1/3]

Q. What is an effective approach for mitigating XSS vulnerabilities?
!Use strong encryption
A. Encode all untrusted input that will be rendered by the browser
!Perform blacklist input validation

XSS code is executed in the browser. As a result, untrusted data must be encoded before it is rendered in the browser itself, which is the correct answer. Input validation is useful as a defense in depth measure to prevent inappropriate characters from being entered in the first place. However, output encoding is the most effective approach for preventing XSS vulnerabilities.

Q. Why do you need to perform contextual output encoding?
!DOM-based XSS can change the encoding format.
A. Untrusted data must be changed into a benign form.
!Blacklists allow certain characters used in XSS attacks.

The correct answer is that untrusted data must be changed into a benign form. Contextual output encoding must be done to ensure that the browser does not treat data as code for execution. This means that a different encoding must be applied for data used in HTML, HTML attribute, URL, CSS, and JavaScript contexts.

Q. What can an attacker do with Cross-Site Scripting (XSS)?
!Conduct intranet port scanning
A. Both of these actions
!Steal session tokens

XSS is a powerful issue that allows attackers to conduct a number of malicious activities by executing arbitrary JavaScript code. The correct answer is that an attacker can do anything that JavaScript allows. This includes conducting intranet port scans, stealing sessions tokens, launching phishing attacks, logging all keystrokes that the user types, and other malicious activities.

# OWA A8 Insecure Deserialization

Serialization:  
The process of transforming arbitrary data into a standard form, usually printable ASCII, so that it can be transported easily

Deserialization:  
The process of decoding the serialized data into it's orginal format

Google, Facebook and OATH 


## Best Practices
- Avoid serialization/deseralization for security
- Consider using a serialized, encrypted token
- Or encrypted and signed token

Q. When using signed tokens, why must the signing key be strong and well protected?
A. If the signing key is easily guessable or otherwise disclosed, it becomes trivial to generate fraudulent requests.
!If the signing key is easily guessable or otherwise disclosed, the administrator account is automatically compromised.
!If the signing key is easily guessable or otherwise disclosed, the user may upload replacement application code.

The correct answer is that if the signing key is easily guessable or disclosed, it becomes trivial to generate fraudulent requests. When signed, serialized, tokens are used for API requests, these tokens are trusted implicitly for authentication/authorization purposes. If the signing key is compromised, an attacker can generate any request while posing as any user, since he can now "authorize" any fraudulent request.

Q. Which of the following is a common use for cryptographically signed serialized tokens?
!Providing a trusted hash of the serialized data, allowing the server-side API endpoints to process the data with no validation, offloading this work to the web client.
!Using the token as an encryption key within the web front end, allowing data to be sent securely even when the communication channel is unencrypted.
A. Passing the token in requests to backend services that are signed or otherwise authenticated, allowing for strong authentication while remaining scalable.

Cryptographically signed tokens are frequently used as authentication tokens in API requests to backend services, which is the correct answer. Using these strongly signed tokens allows the backend service to "trust" the identity information in the token, providing authentication, while eliminating the need for backend, cross-service requests to look up user rights or other authorizations. This allows the backend APIs to be easily scaled.

Q. Which of the following is a common use of serialized data in a web application?
!Streaming real-time video data to the web browser for display
A. Maintaining user input and state across a set of multi-stage forms
!Providing strong encryption capabilities within the browser

The correct answer is maintaining user input and state across a set of multi-stage forms. Common uses for serialized data include things such as application state, session state, multi-form input state, and more within the web application environment. It provides a consistent interface for the transfer of arbitrary data.


# OWA A9 Using Components With Known Vulnerabilities

Tools:
## [OWASP Dependency-Check](https://www.owasp.org/index.php/OWASP_Dependency_Check)

Q. Which of the following is a typical way that vulnerable third-party components end up being used in web applications?
A. The development team imports a set of components that are either vulnerable themselves or make use of other vulnerable components.
!The development team improperly delegates the development of critical components to inexperienced developers, leading to vulnerabilities.
!The development team fails to properly import input validation on all internally developed components, creating known vulnerabilities.

The correct answer is that the development team imports a set of components that are either vulnerable themselves or make use of other vulnerable components. At the root of this issue is importing packages, libraries, or components with preexisting vulnerabilities into the developed application. These could be in the imported library itself, or possibly in some underlying component that the library uses.

Q. How can the OWASP Dependency Check tool help your team?
A. It can provide reports detailing specific vulnerable components that our applications rely on.
!This tool can be used to automatically update all dependencies for non-breaking changes.
!The OWASP Dependency Check tool can act as a WAF, defending vulnerable components.

The OWASP Dependency Check tool can analyze our web application, identifying all underlying components and dependencies that our applications rely on, which is the correct answer. Once it determines the versions that are in use, it will compare this to known vulnerability/version information to create a clear report on vulnerable components.


Q. Why is it impractical to claim that no third-party components will be used to develop a web application?
!Third-party components must be used to prove responsive web applications.
A. This can significantly increase development time and overhead, with no guarantee of more secure code.
!Third-party components frequently contain controlled intellectual property that we cannot legally duplicate.

While it is certainly possible to develop an application without using any third-party components, the correct answer is that this will significantly increase the costs associated with development, in addition to increasing the time required. This development path might be acceptable, but there is still no guarantee that the code will be more secure.

# OWA A10 Insufficient Logging and Monitoring

Q. Which of the following best describes how effective logging and analysis defends the organization?
A. It creates the potential for us to detect misuse and abuse early.
!It provides a guarantee that compromises will no longer succeed.
!It provides strong controls for tracking administrator activities.

The correct answer is that it creates the potential for us to detect misuse and abuse early. Following this best practice gives us the ability to potentially detect and react to misuse and abuse, possibly even compromise, sooner and more effectively.

Q. What value is there in performing correlation within our application?
A. Our application is in the best position to fully understand the relationship of requests.
!Since our application creates the log, it can more rapidly analyze the data.
!There is no value in creating correlation and analysis within the web application.

The correct answer is that our application is in the best position to fully understand the relationship of requests. A great deal of effort is required to automate correlation from discrete log entries from the web application in the event monitoring tool. However, the web application developer is in a much better position to understand the relationships between the types of requests that are being made, allowing for easier misuse and abuse detection.

Q. In addition to generating logs, what other activity must our organization invest in that is most directly connected with this OWASP Top Ten issue?
A. Reviewing the logs
!Correlating compromises
!Processing transactions

Many organizations have enormous logs, but if we never review or analyze the logs, they cannot help us. Therefore, reviewing the logs is the correct answer.


# Application Security: Mobile Development Curriculum  
***

# MOB 01 Insecure Data Storage  


Q. During a requirements meeting, an auditor asks the project team to perform a data classification exercise. Which of the following data elements is permitted to be stored on a mobile device if encrypted at rest?
!User's account password
!Credit card verification code
A. Bank account number

The correct answer is the bank account number. It is the only value that may be stored if properly protected. Avoid storing a user's account password without adaptive hashing protection. Instead, store an authentication token that can be revoked on the server-side. Credit card verification codes are not allowed to be stored at all, especially on a mobile device.

Q. Consider a social media app that has a "remember me" feature that allows users to automatically sign in to their account. Which of the following mobile data storage strategies provides the best security for users?
!Storing the username and password in the device key store.
!Storing an authentication token in the app's data directory.
A. Storing an authentication token in the device key store.

The correct answer is storing authentication tokens that can later be revoked in the device key store offers secure device data storage and process isolation. The app data directory may be encrypted with operating system protections; however, this can be bypassed. Storing username and password values on a mobile device should be avoided, even in the device key store.

Q. Which of the following defenses provides the most protection for sensitive values consumed by a mobile app?
!Storing sensitive values in a properties file with custom encryption.
A. Storing sensitive values on the server side and accessing over a secure API.
!Storing sensitive values in the key store with fingerprint authorization.

Storing values on the server side is the correct answer and best defense because no sensitive data is stored at rest on the device. The other options could allow malware, memory inspection, reverse engineering, or rooting to discover the sensitive information.

Q. Which of the following mobile device data storage locations commonly contains sensitive information stored insecurely by an app?
A. SQLite database files
!HTML5 browser cache
!Keychain database file

The correct answer is SQLite database files. These are the most common storage area for mobile apps and commonly contain sensitive information. HTML5 cache files do not contain data stored and processed by the mobile app (only web views). The keychain database is encrypted and protected with process isolation and the secure enclave.


Q. Consider a healthcare app installed on a non-rooted device with data encryption enabled. The app stores patient information in a custom file inside the app's sandbox directory. Which of the following could allow an attacker to gain access to the patient information?
!Installing an app that reads from the healthcare app's data directory.
Failing to obfuscate the app's source code before uploading to the app store.
Exploiting a vulnerability in the operating system to root the device.

# MOB 02 Unintended Data Leakage

Q. Audit logging is an important countermeasure for defending apps and providing an audit trail of actions. Which of the following is a common shared mobile logging location attackers and malicious apps will search for sensitive data?
!App-specific log files
A. System log files
!HTML5 log files

The system log file is a shared location on mobile devices, which is the correct answer. App-specific and HTML5 logs are not in a shared location.

Q. Which of the following caching vulnerabilities would allow an attacker to find screenshots containing sensitive information on the file system?
!Clipboard sniffing
A. Application backgrounding
!Keyboard auto-complete

Application backgrounding is the correct answer as it automatically stores screenshots in the app's data directory file system, which may contain an app's sensitive information. Keyboard auto-complete and clipboard sharing do not store screenshots.

Q. Consider a mobile app that allows users to register a new account. Part of the registration process requires the user to enter a number of challenge questions and answers. Which of the following caching vulnerabilities is likely to occur when typing the answer to a challenge question?
!System log caching
!URL caching
A. Keyboard caching

The correct answer is keyboard caching. Values entered into text fields are automatically included in keyboard/auto-complete dictionaries, which is likely to include the answers to challenge questions. URL caching contains HTTP response data, not request parameters. The system log cache is unlikely to include keystroke data.

# MOB 03 Broken Cryptography


Secure Secrets Management  

Q. Consider a mobile app that must store secrets on a mobile device. Which of the following benefits does the device keychain/key store offer over storing the key in the app's data directory?
A. Fingerprint Verification
!Encryption
!Secure Data Caching

Fingerprint verification is the correct answer. Both iOS and Android offer encryption and fingerprint authorization on data stored in the keychain and key store. The app sandboxes only offer data encryption on secure non-rooted/non-jailbroken devices. Secure data caching is not related to secrets storage.

Q. Consider a mobile app that needs to generate random data keys for encrypting files at rest on the file system. Which of the following algorithms should be used to generate the random data key value?
A. Cryptographic Random Number Generators
!Pseudo-Random Number Generators
!Symmetric Random Number Generators

Cryptographic Random Number Generators is the correct answer. They are available in all mobile operating systems and produce cryptographically random output. PRNGs produce statistically random numbers that are repeatable. Symmetric Random Number Generators do not exist.

Q. A mobile app development team is building requirements for a new app that will handle top secret data. Which of the following algorithms is not approved for use by The National Institute of Standards and Technology (NIST) and the Open Web Application Security Project Cryptography Guide?
!AES
DES
3DES


Q. Which of the following encryption processes allows the master encryption key to be changed without re-encrypting the data?

!Asymmetric encryption 
A. Envelope encryption
!Symmetric encryption

Envelope encryption is the correct answer. It uses a master key and data key relationship to protect a secret. Changing the master key does not require the data to be decrypted, only the data key itself. Symmetric and asymmetric encryption algorithms alone will require data to be decrypted.

Q. Mobile apps often use adaptive hashing to transform user-supplied input into a cryptographically strong value that uses the entire key space. Which of the following properties of adaptive hashing increases the time required to compute the value?
!Random Salt
A. Adjustable Iterations
!Master Key

Adjustable iterations is the correct answer. The work factor, or number of iterations, increases the time required to compute the hash value. This makes it more difficult for attackers to crack hashes during cryptanalysis. The random salt does not increase computation time, only adds randomness to the hashing process. The master key is the output from the adaptive hashing process.


# MOB 04 Client-Side Injection

Object Relational Mapping

## Local File Inclusion

Q. Consider a mobile banking app that displays HTML content in a web view. A customer informs the security team that the account information screen displayed a number of popup alerts asking them to enter sensitive information. Which of the following mobile client side injection vulnerabilities was likely used to attack the customer?
!XML Injection
!SQL Injection
A. JavaScript Injection

JavaScript Injection is the correct answer. Mobile web views are vulnerable to JavaScript Injection, also known as cross-site scripting attacks, similar to web browsers. In this case, the web view failed to output encode its data, resulting in JavaScript execution on the device. SQL Injection does not run script in a web view, and XML injection is not discussed in the module.

Q. Consider an insurance app that displays data from a web service API in an HTML web view. A mobile penetration test reveals this screen is vulnerable to JavaScript Injection. Which of the following defenses can be used to remediate the JavaScript Injection vulnerability?
A. Output Encoding
!Server-side Authorization
!Blacklist Input Validation

The correct answer is Output Encoding. Mobile applications rendering untrusted data in a web view should perform context-specific output encoding, such as HTML, JavaScript, and URL encoding, before displaying it to the user. Input validation only helps if the data is entering the application through the web view. In this case, the data is coming from the server. Server-side authorization does not help defend against JavaScript Injection.

Q. Consider a coupon mobile app that stores a number of coupons in the app's data directory. The mobile app displays the coupon of the day in a web view that has access to the file system. Which of the following vulnerabilities could be used to gain unauthorized access to the coupon files?
!Cross-site Scripting
A. Local File Inclusion
!SQL Injection

The correct answer is Local File Inclusion. Web view parameters can be modified to read files from the mobile app's file system. SQL Injection attacks are not guaranteed to have access to the mobile app file system. Cross-site scripting attacks are browser-based attacks.

# MOB 05 Reverse Engineering

Tools:
- [DexGuard](https://www.guardsquare.com/en/products/dexguard)


Q. Consider the following mobile apps. Which app should spend more effort to defend against reverse engineering?
A. A healthcare and prescription app
!A solitaire card game playing app
!A sports score keeping app

The correct answer is a healthcare and prescription app. Apps that process sensitive user information, contain intellectual property, or are deemed essential for a corporate brand should spend more effort to defend against reverse engineering. Healthcare apps typically contain larger amounts of sensitive user data and should spend more effort in preventing reverse engineering than apps that only manage game scores, data feeds, and other non-security related features.


Q. When should automated tools be used to test a mobile app's resistance to reverse engineering?
!Only when manual testing is not possible due to code complexity.
!After the last user acceptance testing has been performed.
A. During the full development lifecycle and testing process.

Automated tools should be leveraged during the full development lifecycle and testing process, which is the correct answer. This helps development teams detect and eliminate obvious flaws that would otherwise be detected by an attacker. Automated tools are not a replacement for manual testing. Both automated and manual testing have their pros and cons and should be used in conjunction to provide the best security coverage for an app.

Q. Consider the following mobile device configurations. Which one should a development team check for to minimize the risk of reverse engineering?
!The device requires a PIN or password to log in.
A. The device has been rooted or jailbroken.
!The device has enabled full-disk encryption.

The correct answer is the device that has been rooted or jailbroken. Mobile devices that have been rooted or jailbroken are at an increased risk, as exploits are easier to install and execute on them. As such, development teams should check for rooting/jailbreaking and shut their app down if this configuration is detected. Using full-disk encryption and requiring a PIN or password for device access are good controls to prevent other types of security risks, but do not affect the risk of reverse engineering.


# Application Security: Defensive Coding Curriculum
***

Memory Inspection

Q. What memory inspection defense does a mutable object type, such as a character array, provide to development teams?
!Mutable objects use randomized address space layout
A. Mutable objects allow their values to be destroyed
!Mutable objects encrypt their data in memory

Q. Which of the following object types is immutable, meaning it cannot be programmatically cleared from memory after being created?
!Character Array
A. String
!SecureString

Q. Which of the following options can be used to protect symmetric encryption keys from memory inspection issues?
A. Storing keys in a location separate from the data being protected
!Granting admin accounts read access to the key store
!Using immutable object types to make keys easily accessible


# Cross Site Request Forgery
CSRF  
XSSRF  

Tools: 
- OWASP CSRFGuard Project  
  https://www.owasp.org/index.php/Category:OWASP_CSRFGuard_Project

- OWASP Enterprise Security API
  https://www.owasp.org/index.php/Category:OWASP_Enterprise_Security_API


Q. Which of the following is a possible method for protecting against CSRF attacks?
A. Require that the user reauthenticate before allowing any significant action to be processed.
!Use strong input validation and sanitization through whitelisting.
!Ensure that the user authentication process uses HTTPS.
!Always put the session token in the URL.


Q. CSRF attacks:
A. May occur without the user ever realizing it, as a result of hidden frames or image tags.
!Are always visible to the end user when they occur.
!Are impossible to mitigate.
!Require that JavaScript is enabled on the end user’s browser to be effective.

Q. CSRF takes advantage of the fact that:
Cookies are easily exposed using a sniffer.
It is the browser or the deputy that is authenticated, not the user.
Cookies are not encrypted on the local disk of a workstation.
!Reflected JavaScript attacks are easy to launch when input is not properly sanitized.

Q. CSRF is also referred to as:
A. Confused Deputy.
!Cross Site Scripting.
!Deputy Dog.
!Confused Marshal.

Q. Which of the following is a possible method for protecting against CSRF attacks?
!Require the user to disable JavaScript on his browser.
A. Including a random token specifically for CSRF protection in every request.
!Use encryption for all transactions in which sensitive data is handled.
!Use a cryptographically strong and extremely long session ID to prevent hijacking.


# Unvalidated Redirects and Forwards

Q. Which of the following is a primary reason for the use of a redirect or forward function in an application?
!The certificate expired before a new one was installed, requiring that all of the former requests be redirected to the new certificate.
!The IP address of the server has changed, requiring all of the URLs to be updated.
!There is no good reason for using a redirect function.
A. The application has evolved over time and resources have moved to new locations within the site.

Q. If our application implements a redirect function it is important to:
!Use good input sanitization to prevent cross site request forgery.
!Ensure that TLS is used consistently.
A. Ensure that the function will only redirect users to specific URLs.
!Allow the redirect function to be used to send the user anywhere on the Internet.


Q. One of the main ways that unvalidated redirects and forwards can be used against our users is:
!Exposure of session tokens.
!Improper use of encryption technologies.
A. Social engineering and phishing attacks.
!Ability to sniff contents of sensitive communications off of the network.