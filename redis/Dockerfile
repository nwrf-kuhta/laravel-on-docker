FROM redis:6.0.6
LABEL maintainer="nwrf.kuhta <nwrf.kuhta@gmail.com>"

# Set the timezone.
RUN /bin/cp -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Copy the redis.conf
COPY ./redis.conf /usr/local/etc/redis/redis.conf

# Start the proccess.
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
