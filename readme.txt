Description:
------------

vBulletin addon to make direct thumbnail links and fast attachments download via nginx.
Significantly reduce server load.

Installation
------------

1. Import XML file
2. Change addon settings to fit your site
3. Update webserver config
    - add rewrites
    - !!! add cache expires time, to remove 304 requests
    - add gzip for CSS/JS 

Nginx config sample:

====
# Modified gzip settings: added CSS/JS,
# but completely disabled for broken browsers.
gzip_types       text/plain text/css application/x-javascript text/xml text/javascript;
gzip_disable     "MSIE [1-6].(?!.*SV1)";


# globally disable external access to attachments, but enable for X-Accel-Redirect
location /uploads {
    internal;
}
# enable thumbnails direct access, but nothing else!
location ~* /uploads/(.*)\.thumb$ {
    expires 24h;
}


# Expires for static files
location /images/ {
    expires 24h;
}
location /clientscript/ {
    expires 24h;
}
location /custom { # All at once: profile pics, avatars, group images
    expires 24h;
}
====

Released at vborg:
http://www.vbulletin.org/forum/misc.php?do=producthelp&pid=vb_accelerator
