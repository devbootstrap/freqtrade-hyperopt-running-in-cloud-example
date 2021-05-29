# Folder for Diffie-Hellman key

This folder `dhparam` will contain the Diffie-Hellman key on the server. To generate a new key, run the following command:

```
cd ft_userdata
sudo openssl dhparam -out dhparam/dhparam-2048.pem 2048
```

When you are done you can restart the webserver service using:

```
docker-compose up -d --force-recreate --no-deps webserver
```