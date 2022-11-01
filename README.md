# Laravel with XDEBUG

##

RUN `sail artisan sail:publish`

Create a file `.vscode/launch.json`

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "log": false,
            "externalConsole": false,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}"
            },
            "ignore": ["**/vendor/**/*.php"],
            "port": 9003
        }
    ]
}
```

Create a file `./docker/8.1/ext-xdebug.ini`

```conf

[xdebug]
xdebug.start_with_request=yes
xdebug.discover_client_host=true
xdebug.max_nesting_level=256
xdebug.remote_handler=dbgp
xdebug.client_port=9000
xdebug.idekey=VSCODE
xdebug.mode=debug
xdebug.client_host=host.docker.internal

```

On the file `docker/8.1/Dockerfile` before the command `RUN chmod +x /usr/local/bin/start-container` insert the following command:

-   `COPY ext-xdebug.ini etc/php/8.1/cli/conf.d/ext-xdebug.ini`

Run

```bash
sail artisan build --build -d
```
