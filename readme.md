1. The Vagrant should be installed.
2. Clone this repo into a directory on your computer.
3. Open the Terminal in that directory and generate a key pair using the "ssh-keygen" command (use ./key on the "Enter file in which to save the key" prompt).
4. vagrant up
5. vagrant ssh VM1
6. ansible-playbook /vagrant/playbook.yml
7. check http://192.168.10.10:8080/app.php
