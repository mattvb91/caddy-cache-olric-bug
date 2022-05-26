

```bash
# up to see log
docker-compose up

```

Then fire a request at admin to change the config

```bash
curl --location --request POST 'localhost:2019/load' \
--header 'Content-Type: application/json' \
--header 'host: localhost' \
--data-raw '{
  "admin": {
    "listen": ":2019"
  },
  "apps": {
    "cache": {
      "api": {
        "basepath": "/__cache",
        "souin": {
          "basepath": "/souin",
          "enable": true
        }
      },
      "distributed": true,
      "log_level": "debug",
      "ttl": "3600s"
    },
    "http": {
      "servers": {
        "server1": {
          "listen": [
            ":80"
          ],
          "routes": [
            {
              "handle": [
                {
                  "allowed_http_verbs": [
                    "GET"
                  ],
                  "default_cache_control": "no-store",
                  "handler": "cache"
                },
                {
                  "body": "caddy is working",
                  "handler": "static_response",
                  "status_code": 200
                }
              ]
            }
          ]
        }
      }
    }
  },
  "logging": {
    "logs": {
      "default": {
        "level": "INFO"
      }
    }
  }
}'
```