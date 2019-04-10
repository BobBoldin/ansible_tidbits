### Sample Run ###
'''
ansible-playbook test_role.yml 
 [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [test] ******************************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [my_containers : Containers before Modification] ************************************************************************************************************************************************************************************
ok: [localhost] => {
    "containers": {
        "grafana": {
            "image": "grafana/grafana:6.0.0", 
            "networks": [
                "grafana-network", 
                "traefik-network"
            ], 
            "ports": "3000:3000", 
            "secrets": {
                "GF_AUTH_GENERIC_OAUTH_CLIENT_SECRET": "https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery4/ff177dcf5a734ad69563908fdcb45933", 
                "GF_DATABASE_PASSWORD": "https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery3/ff177dcf5a734ad69563908fdcb45933", 
                "GF_SECURITY_ADMIN_PASSWORD": "https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery1/ff177dcf5a734ad69563908fdcb45933", 
                "GF_SESSION_PROVIDER_CONFIG": "https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery2/ff177dcf5a734ad69563908fdcb45933"
            }, 
            "variables": {
                "docker": [
                    {
                        "GF_INSTALL_PLUGINS": "grafana-azure-monitor-datasource,grafana-azure-data-explorer-datasource"
                    }, 
                    {
                        "GF_SESSION_PROVIDER": "postgres"
                    }, 
                    {
                        "GF_DATABASE_TYPE": "postgres"
                    }, 
                    {
                        "GF_DATABASE_HOST": "redacted.postgres.database.azure.com"
                    }, 
                    {
                        "GF_DATABASE_NAME": "grafana"
                    }, 
                    {
                        "GF_DATABASE_USER": "sysadmin@prometheus-monitoring-postgresql"
                    }, 
                    {
                        "GF_SERVER_ROOT_URL": "https://grafana.production.redacted/"
                    }, 
                    {
                        "GF_DATABASE_SSL_MODE": "require"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_ENABLED": true
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_ALLOW_SIGN_UP": true
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_CLIENT_ID": "redacted"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_SCOPES": "openid email profile"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_AUTH_URL": "https://login.microsoftonline.com/redacted/oauth2/v2.0/authorize"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_TOKEN_URL": "https://login.microsoftonline.com/redacted/oauth2/v2.0/token"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_API_URL": "https://graph.microsoft.com/oidc/userinfo"
                    }
                ]
            }, 
            "volumes": [
                "/data/docker-data/grafana/conf/:/var/lib/grafana/"
            ]
        }, 
        "prometheus": {
            "cmd": "--storage.tsdb.path=/prometheus", 
            "image": "prom/prometheus:v2.6.0", 
            "networks": [
                "grafana-network", 
                "traefik-network"
            ], 
            "ports": "9090:9090", 
            "secrets": {
                "PROM_PWD1": "https://MYVAULT.vault.azure.net/secrets/prom1/ff177dcf5a734ad69563908fdcb45912", 
                "PROM_PWD2": "https://MYVAULT.vault.azure.net/secrets/prom2/ff177dcf5a734ad69563908fdcb45911"
            }, 
            "user": "root", 
            "volumes": [
                "/data/sadisk/prometheusmonitoring/shared/prometheus/conf/:/etc/prometheus/", 
                "/data/datadisk/docker-data/prometheus/data:/prometheus"
            ]
        }
    }
}

TASK [my_containers : Configure defined containers] **************************************************************************************************************************************************************************************
included: /home/rboldin/projects/ansible_tidbits/muhaha/roles/my_containers/tasks/create_container.yml for localhost => (item=prometheus)
included: /home/rboldin/projects/ansible_tidbits/muhaha/roles/my_containers/tasks/create_container.yml for localhost => (item=grafana)

TASK [my_containers : set_fact] **********************************************************************************************************************************************************************************************************
ok: [localhost] => (item={'key': u'PROM_PWD2', 'value': u'https://MYVAULT.vault.azure.net/secrets/prom2/ff177dcf5a734ad69563908fdcb45911'})
ok: [localhost] => (item={'key': u'PROM_PWD1', 'value': u'https://MYVAULT.vault.azure.net/secrets/prom1/ff177dcf5a734ad69563908fdcb45912'})

TASK [my_containers : set_fact] **********************************************************************************************************************************************************************************************************
ok: [localhost] => (item={'key': u'GF_SECURITY_ADMIN_PASSWORD', 'value': u'https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery1/ff177dcf5a734ad69563908fdcb45933'})
ok: [localhost] => (item={'key': u'GF_AUTH_GENERIC_OAUTH_CLIENT_SECRET', 'value': u'https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery4/ff177dcf5a734ad69563908fdcb45933'})
ok: [localhost] => (item={'key': u'GF_SESSION_PROVIDER_CONFIG', 'value': u'https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery2/ff177dcf5a734ad69563908fdcb45933'})
ok: [localhost] => (item={'key': u'GF_DATABASE_PASSWORD', 'value': u'https://MYVAULT.vault.azure.net/secrets/grafana-aad-discovery3/ff177dcf5a734ad69563908fdcb45933'})

TASK [my_containers : Containers after Modification] *************************************************************************************************************************************************************************************
ok: [localhost] => {
    "containers": {
        "grafana": {
            "image": "grafana/grafana:6.0.0", 
            "networks": [
                "grafana-network", 
                "traefik-network"
            ], 
            "ports": "3000:3000", 
            "secrets": {
                "GF_AUTH_GENERIC_OAUTH_CLIENT_SECRET": 24, 
                "GF_DATABASE_PASSWORD": 74, 
                "GF_SECURITY_ADMIN_PASSWORD": 77, 
                "GF_SESSION_PROVIDER_CONFIG": 47
            }, 
            "variables": {
                "docker": [
                    {
                        "GF_INSTALL_PLUGINS": "grafana-azure-monitor-datasource,grafana-azure-data-explorer-datasource"
                    }, 
                    {
                        "GF_SESSION_PROVIDER": "postgres"
                    }, 
                    {
                        "GF_DATABASE_TYPE": "postgres"
                    }, 
                    {
                        "GF_DATABASE_HOST": "redacted.postgres.database.azure.com"
                    }, 
                    {
                        "GF_DATABASE_NAME": "grafana"
                    }, 
                    {
                        "GF_DATABASE_USER": "sysadmin@prometheus-monitoring-postgresql"
                    }, 
                    {
                        "GF_SERVER_ROOT_URL": "https://grafana.production.redacted/"
                    }, 
                    {
                        "GF_DATABASE_SSL_MODE": "require"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_ENABLED": true
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_ALLOW_SIGN_UP": true
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_CLIENT_ID": "redacted"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_SCOPES": "openid email profile"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_AUTH_URL": "https://login.microsoftonline.com/redacted/oauth2/v2.0/authorize"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_TOKEN_URL": "https://login.microsoftonline.com/redacted/oauth2/v2.0/token"
                    }, 
                    {
                        "GF_AUTH_GENERIC_OAUTH_API_URL": "https://graph.microsoft.com/oidc/userinfo"
                    }
                ]
            }, 
            "volumes": [
                "/data/docker-data/grafana/conf/:/var/lib/grafana/"
            ]
        }, 
        "prometheus": {
            "cmd": "--storage.tsdb.path=/prometheus", 
            "image": "prom/prometheus:v2.6.0", 
            "networks": [
                "grafana-network", 
                "traefik-network"
            ], 
            "ports": "9090:9090", 
            "secrets": {
                "PROM_PWD1": 44, 
                "PROM_PWD2": 11
            }, 
            "user": "root", 
            "volumes": [
                "/data/sadisk/prometheusmonitoring/shared/prometheus/conf/:/etc/prometheus/", 
                "/data/datadisk/docker-data/prometheus/data:/prometheus"
            ]
        }
    }
}

PLAY RECAP *******************************************************************************************************************************************************************************************************************************
localhost                  : ok=7    changed=0    unreachable=0    failed=0
'''
