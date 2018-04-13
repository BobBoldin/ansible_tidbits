Setup
-----

Add the contents of the file: etc_hosts_all_pass to your /etc/hosts

```
192.68.241.207 ws-sips.cluster.local
192.68.241.173 ws-coffee.cluster.local
```

Run the Playbook
----------------

From the blog1 directory run

    ansible-playbook -i hosts check_etc_hosts.yml -e "target=localhost"

Both tests should pass

Alternate 1
-----------

Edit /etc/hosts and change one of the ipv4 entries

Re-running the playbook should result in an error MSG similiar to

    Entry IP mismatch ws-sips.cluster.local Expected 192.68.241.207 Received [u'192.68.241.208']


Alternate 2
-----------

Edit /etc/hosts and remove 1 of the entries

Re-running the playbook should result in an error MSG of 

    One or more supplied key could not be found in the database.
