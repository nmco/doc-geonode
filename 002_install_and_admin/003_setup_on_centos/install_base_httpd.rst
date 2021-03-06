.. _install_base_httpd:

===============================
Apache HTTP Server Installation
===============================


Install Apache::

    sudo yum install -y httpd

And additional modules::

    sudo yum install -y mod_ssl mod_proxy_html mod_wsgi

Firewall configuration
----------------------

Allow requests on port 80 through the firewall::

    firewall-cmd --zone=public --add-service=http --permanent
    firewall-cmd --reload

Security issues
---------------

There are a couple of security issues to fix when dealing with GeoNode.

GeoNode will run inside httpd through WSGI. This means that httpd will try to perform external connection toward the DB.
This is usually blocked by default by strict security policies, so we need to relax them::

   setsebool -P httpd_can_network_connect_db 1

The other issue is about SELinux itself: it is not WSGI friendly, so we'll have to disable it.
Edit the file ``/etc/sysconfig/selinux`` and  change the line::

   SELINUX=enforcing

into ::

   SELINUX=permissive

and reboot the machine.


httpd configuration
-------------------

As ``root`, create the file ``/etc/httpd/conf.d/geonode.conf``
and insert into it :download:`this content <resources/geonode.conf>`.

Add `thumbs` and `layers` folders::

    sudo mkdir -p /home/geonode/geonode/geonode/uploaded/thumbs
    sudo mkdir -p /home/geonode/geonode/geonode/uploaded/layers

Set appropriate permissions on the folders::

    sudo chown -R geonode /home/geonode/geonode/
    sudo chown geonode:www-data /home/geonode/geonode/geonode/static/
    sudo chown geonode:www-data /home/geonode/geonode/geonode/uploaded/
    chmod -Rf 777 /home/geonode/geonode/geonode/uploaded/thumbs
    chmod -Rf 777 /home/geonode/geonode/geonode/uploaded/layers
    sudo chown www-data:www-data /home/geonode/geonode/geonode/static_root/


Then restart httpd to make it reload the new configurations::

   systemctl restart httpd

To automatically start Apache at boot, run::

    systemctl enable httpd
