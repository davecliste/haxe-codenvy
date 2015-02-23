# haxe-codenvy
Haxe docker image - mainly created for use on codenvy.com

##Usage
Create a custom environment/Dockerfile in your codenvy project.

Then replace the contents of the Dockerfile with the following:

```Dockerfile
FROM davecliste/haxe-codenvy

# Add project source files to docker image
ADD         $src$ /home/user/


# compile source files, copy bin/build/output files to apache dir and run apache server
CMD         sudo chown -R www-data:www-data $SITE_DIR/ && \
            sudo chmod -R 777 $SITE_DIR && \
            openfl build flash && \
            cp -R ./bin /var/www/html && \
            sudo service apache2 start && \
            sudo tail -f $APACHE_LOG_DIR/access.log -f $APACHE_LOG_DIR/error.log
```
