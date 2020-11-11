# webhook-receiver
A sample of webhook receiver made with Python
  
## pre-install  
```
yum install mod_wsgi -y
git clone git@github.com:a6350202/webhook-receiver.git /var/www/webhooks
virtualenv /opt/virtualenvs/webhooks
/opt/virtualenvs/webhooks/bin/pip install -r /var/www/webhooks/requirements.txt
```
  
## setup Apache
```
mkdir -p /var/www/static
cd /var/www/static
git clone <remote-repository>
chown -R apache:apache .

cp /var/www/webhooks/vhosts_webhooks.conf /etc/httpd/conf.d/vhosts_webhooks.conf
echo 'Listen <port>' >> /etc/httpd/conf/httpd.conf

service httpd start
chkconfig httpd on
```
  
## setup SSH key
create `apache ssh-key path` first
```
mkdir -p /var/www/.ssh/
cd /var/www/.ssh/
sudo -u apache pwd
```
```
sudo -u apache ssh-keygen -t rsa
cp /var/www/webhooks/config <apache-home-path>
touch /var/www/.ssh/known_hosts

chown -R apache:apache /var/www/.ssh
chmod 700 /var/www/.ssh
```
Hint: Remember to add the `/var/www/.ssh/id_rsa.pub` content in GitHub/GitLab ssh key or deploy key.
