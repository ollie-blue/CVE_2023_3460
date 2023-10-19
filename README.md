# CVE_2023_3460
Exploit wp capabilities and wordPress ultimate member plugin to create admnistrator account

How WordPress treats metadata keys made it possible for attackers to trick the plugin into updating some it shouldn’t, like “wp_capabilities”, which is used to store a user’s role and capabilities. This project tested the possibility of exploiting wp_capabilities and wordPress ultimate member plugin on localhost. Using Burp Suite, this project manipulated the meta value and further fuzz the POST request headers. As a result, it successfully registered a user with the ‘administrator’ role and capabilities.

## Getting Started
These instructions will enable you to test plugin vulnerability on your localhost (See the CVE-2023-3460 doc).
 
### Prerequisites
WordPress (installed)
Xampp (installed)
Some useful links (see References at the bottom of this document)

#### Running the tests
See the CVE-2023-3460 doc.


Keywords:
Unauthenticated Privilege Escalation, WordPress, Burp Suite, ultimate members plugins (versions lower than 2.6.7)

References:
1.	https://wpscan.com/vulnerability/694235c7-4469-4ffd-a722-9225b19e98d7/
2.	www.urldecoder.org
3.	https://www.unserialize.com/



