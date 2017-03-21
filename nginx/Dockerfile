

# Set nginx base image
FROM nginx

# File Author / Maintainer
MAINTAINER Christoph Gebendorfer

# Create SSL directory
RUN mkdir /etc/nginx/ssl

# Create Auth directory
RUN mkdir /etc/nginx/auth

# Copy custom configuration file from the current directory
COPY nginx.conf /etc/nginx/nginx.conf

# Copy nginx.cert and nginx.key (self generated)
COPY nginx.cert /etc/nginx/ssl/nginx.crt
COPY nginx.key /etc/nginx/ssl/nginx.key

# Copy registry.password for docker registry authenication
COPY registry.password /etc/nginx/auth/registry.password
