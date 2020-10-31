FROM mongo:3
ADD ./dbscripts /tmp/dbscripts 

# Modify child mongo to use /data/db-accounts as dbpath (because /data/db wont persist the build because it is already a VOLUME)
RUN mkdir -p /dbscripts\
    && echo "dbpath = dbscripts" > /etc/mongodb.conf \
    && chown -R mongodb:mongodb /dbscripts

RUN su - mongodb && mongod --fork --logpath /var/log/mongodb.log --dbpath /dbscripts  \
    && chmod u+x /tmp/dbscripts/mongo_create_insert.sh / && /tmp/dbscripts/mongo_create_insert.sh \
    && mongod --dbpath /dbscripts --shutdown \
    && chown -R mongodb /dbscripts 

# Make the new dir a VOLUME to persist it
VOLUME /dbscripts

CMD ["mongod", "--config", "/etc/mongodb.conf", "--smallfiles"]

