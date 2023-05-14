Postmortem
Service Failure - Incident Report on Site Outage
Summary
On September 17th, 2023 from 12:30 PM to 1:30 PM WAT, the company's website was down for thirty minutes. 100% of users experienced a 500 internal server error caused by a wrong filename in a configuration file in the NGINX server.
Timeline
12:30 PM Outage begins 12:55 PM Error logs checked by DevOps team 1:10 PM Configuration updated to log extra errors 1:15 PM Filename error caught in config file 1:20 PM Execute Puppet manifest across all company servers 1:30 PM 100% restored and back online
Root Cause and Resolution
After a small sitewide update was deployed without first being tested, an outage to the site began. When no errors were found in our 'error.log' files we modified our configuration file to allow for more error logging. With the help of 'strace,' it appeared an accidental filename misspelling triggered errors when the site was requested. The server was attempting to locate the file as normal procedure but failed to find the file ending in ".phpp" when it should be looking for ".php'' After changing this line in the '/var/www/html/wp-settings.php' file, tests succeeded to show the site. A puppet manifest was written and executed across all company servers immediately after to restore service.
Corrective and Preventative Measures
After a discussion it has been decided we can prevent this in the future by:
Modifying configuration files for more error logging to quicken response times Test before deploying on all servers no matter how small an update.


