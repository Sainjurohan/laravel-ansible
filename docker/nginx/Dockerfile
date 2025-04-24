# Configuring the baseimage that is to be used
FROM nginx:latest

# Setting the Working Directory
WORKDIR /var/www/html/todo

COPY . /var/www/html/todo
# Copying the custom nginx configuration file to the server
COPY docker/nginx/default.conf /etc/nginx/conf.d/default.conf

# Setting the correct permissions
RUN chmod -R 755 /var/www/html

# Exposing the ports for http and https
EXPOSE 5111

# Starting Nginx in the foreground
CMD [ "nginx", "-g", "daemon off;" ]