# Docker-xBrowserSync-api
Docker files to create a xBrowserSync api container

To create the docker image, please download these files into a folder and the execute the following command:

`docker build -t xbrowsersyncdev .`

Once it has been created, please use the following command for execution

`docker exec run -d -p 28080:8080 --name xbrowsersync -v /apps/xbrowsersync/settings.json:/xbrowsersync/config/settings.json xbrowsersyncdev`

where `/apps/xbrowsersync/settings.json` is the route of the settings.json file. 

If you need to run this behind a nginx as reverse proxy, please add the following lines on the nginx confi file

location /xbrowsersync/ {
    auth_basic off;
    rewrite ^/xbrowsersync(/.*)$ $1 break;
    proxy_pass  http://192.168.1.175:28080/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_redirect    off;
}


