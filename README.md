# ckan-config

CKAN code in the AWS EC2 instance in AWS code is at path: 

    /usr/lib/ckan/default/src/ckan

e.g.:

    /usr/lib/ckan/default/src/ckan/ckan/templates/snippets

branch is dkan-ami (should have been ckan-ami) and includes a minor language change. I've modified these two pages:

    /usr/lib/ckan/default/src/ckan/ckan/templates/home/snippets/promoted.htm
    /usr/lib/ckan/default/src/ckan/ckan/public/base/images/placeholder-420x220.pn

This script restarts CKAN on server reboots:

    /root/ckan_init.sh

It is triggered by this file:

    /etc/rc.local

Config file for CKAN is at path:

    /etc/ckan/default/production.ini

Config files for some CKAN servicers are at:

    /etc/supervisord.d

* ckan-uwsgi.conf: configures the uWSGI server process, which serves the CKAN web application
* ckan-worker.conf: configures CKAN’s background worker processes, typically used for handling asynchronous tasks such as sending emails or processing queued jobs
* ckan-harvest.conf:  configures the harvesting process, which collects and imports datasets from external sources

To restart the CKAN-related processes managed by Supervisor:

    supervisorctl restart ckan

To create resource views (visual representations of datasets):

    ckan -c production.ini views create

To activate the CKAN virtual environment:

    . /usr/lib/ckan/default/bin/activate
    echo $VIRTUAL_ENV

The CKAN virtual environment lets you run command such as:

    ckan -c /etc/ckan/default/ckan.ini run

The CKAN harvest extension:

    cd /usr/lib/ckan/default/src/ckanext-harvest
    git remote add sheldon https://github.com/sheldonrampton/ckanext-harvest.git
    git push sheldon master

For CKAN pages:

    cd /usr/lib/ckan/default/src/ckanext-pages/

When I connect to the EC2 instance, I'm user ec2-user:

    cd /home/ec2-user/

Nginx is the webserver:

    ls /var/log/nginx/prod_ckan/
    tail /var/log/nginx/prod_ckan/prod_ckan_error.log
    tail /var/log/nginx/prod_ckan/prod_ckan_access.log
    cd /etc/nginx/
    cat nginx.conf
    cd conf.d/
    cat prod_ckan.conf
    cd ../default.d/
    cd ../ckan/default/
    cat production.ini

Logs are at:

    /var/log/prod_ckan

Content shared on the site is at:

    /var/shared_content/prod_ckan/
    ls /var/shared_content/prod_ckan/resources
    ls /var/shared_content/prod_ckan/sessions/
    ls /var/shared_content/prod_ckan/sessions/container_file
    ls /var/shared_content/prod_ckan/webassets/
    ls /var/shared_content/prod_ckan/webassets/base/
    ls /var/shared_content/prod_ckan/webassets/ckanext-geoview/
    ls /var/shared_content/prod_ckan/webassets/ckanext-harvest/
    ls /var/shared_content/prod_ckan/webassets/ckanext-pages/
    ls /var/shared_content/prod_ckan/webassets/ckanext-reclineview/
    ls /var/shared_content/prod_ckan/webassets/vendor/
