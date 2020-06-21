# Portfolio
Building a portfolio using WordPress, hosted on AWS.

1. Make an AWS account
2. Go to Management Console
3. Go to services
4. Click EC2
5. Search for WorkdPress in marketplace, and choose the one at the top, WordPress +Bitnami, Debian

6. Select it, and choose an instance type (General Purpose t2.micro)
7. Review and launch.
8. Create Key Value Pair (.pem), save it
9. Launch instances
10. Click on instance id (i-xxxxxxxx...)

11. Name your instance, probably with your domnain name. Yes, buy a domain name too.
12. Note down your public ip: 18.224.39.155 (for krishanuskr.com)
13. Search for Route 53 in Services
14. Go to DNS Management, and create a Hosted Zone
15. Add your domain name (krishanuskr.com)

16. Note the DNS names: 
	ns-7xx.awsdns-27.xxx.
	ns-4xx.awsdns-57.xxx.
	ns-1xxx.awsdns-32.xxx.
	ns-1xxx.awsdns-47.co.xx.
  
17. Create record set. Add "wwww" to name, Leave TTL to 300 seconds if you plan to make DNS changes, or make it 24 hours if not. I left it at 300, will edit after further consultation. Put the public ip in Value.
18. Create another record set without "www", and same ip.
19. Copy the DNS names saved in 16th point in Nameservers without the dot(.) in the end.
20. Removed the following pre-existing nameservers:
    Eg: ns1.domain.com
    	  ns2.domain.com

21. Website is live, or should be live in 24 hours. Works with VPN almost immediately, might take time for Indian ISPs, while you get a     403.
22. Go to EC2. Right click on the instance. Go to Instance Settings -> System Logs -> go to almost the bottom to get username and           password. 
	  Deafault username is 'user'.
23. Go to <yourdomain>.com/wp-login and enter the credentials
24. Download PuTTY for free ssl certificate. From puttygen, load your key value pair (pem file), and generate the ppk file.
25. Go to putty. Go to Session. Enter IP of your website: 18.224.39.155. Create a session name, probably with the kind of website it is.     I named it krishanuskr portfolio.  
  
26. Click on SSH->Auth->browse the ppk file.
27. Click on Connection->Data, Auto login username: bitnami Don't click on open.
28. Go back to session. click on session name, and save it.
29. Double click on the session name to open the bitnami command line
30. enter: sudo /opt/bitnami/bncert-tool and follow the on-screen instructions. This is Bitnami HTTPS Configuration Tool.

31. Next, to access myadmin in php: go to putty. In session, select your session and load. 
32. Next, go to Connection -> SSH -> Tunnel -> Source Port=8888, Destination=localhost:80. Click on add.
33. Go to Session, save it. Open the session now.
34. After the bitnami command line opens up, go to the browser and type http://localhost:8888/phpmyadmin/
35. username is 'root', password is same as bitnami System Logs.

36. Click on bitnami wordpress in the left column
37. Download, set up WinSCP tool.
38. Don't import. Choose SFTP, enter ip address, user as bitnami and password as 5vsDl7HXBRJP. Save it for the future, and login to view     ftp.
39. To remove the bitnami tag from the web page:
    sudo /opt/bitnami/apps/wordpress/bnconfig.disabled --disable_banner1
40. That should be it. Go on to <yourdomain>.com/wp-login to design your website.
