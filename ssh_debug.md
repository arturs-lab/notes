## This trick helped me debug ssh connectivity issue
I waqs having trouble connecting to remote server from GUI client which did not offer much in terms of logging or debug output. I've found [this article](https://stackoverflow.com/questions/47875126/we-did-not-send-a-packet-disable-method) helpful. 

Start new sshd session with debug enabled<br>
```/usr/sbin/sshd -d -p 2222```<br>
connect to that session from client and observe behavior
