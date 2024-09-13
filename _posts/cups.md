sudo systemctl restart cups

remote access cups through web

3 methods:

1.
cupsctl --remote-admin --remote-any --share-printers
it will update the /etc/cups/cupsd.conf file and restart cups for you, saving a backup of the previous configuration in the same folder.

http://www.cups.org/documentation.php/doc-2.0/sharing.html

2.
ssh admin@10.36.8.43 -T -L 3631:localhost:631

3.
http://thismightbehelpful.blogspot.com/2008/09/remote-access-tocups-web-interface.html
Allow all to <Location /admin>

Allow from 192.168.8.114  #a certain computer
Allow from 192.168.8.*    #subnet
