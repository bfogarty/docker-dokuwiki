DokuWiki Docker Container
========================

DokuWiki container with URL rewrite, authad, and X-Sendfile support.

For pretty URLs, go to the Configuration Manager and set userewrite to ".htaccess"

To enable the X-Sendfile header, go to the Configuration Manager and set xsendfile to "Proprietary lighttpd header"

For AD authentication, enable the [authad](https://www.dokuwiki.org/plugin:authad) plugin.

To run:
-------

    docker run -d -p 80:80 --name dokuwiki bfogarty/dokuwiki

The installer will then be accessible at: <http://localhost/install.php>

To make data persistent:
------------------------

Create a data container:

    docker run --volumes-from dokuwiki --name dokuwiki_data busybox true

Now you can safely delete your DokuWiki container:

    docker stop dokuwiki && docker rm dokuwiki

To recreate your DokuWiki container, attach the volumes from your dokuwiki_data container:

    docker run -d -p 80:80 --name dokuwiki --volumes-from dokuwiki_data bfogarty/dokuwiki

To build:
--------

    git clone https://github.com/bfogarty/docker-files.git
    cd docker-files/dokuwiki
    docker build -t bfogarty/dokuwiki .
