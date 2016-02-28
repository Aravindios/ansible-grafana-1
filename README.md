grafana
=======

Installs and configures Grafana.

Requirements
------------

[![Build Status](https://travis-ci.org/kbrebanov/ansible-grafana.svg?branch=master)](https://travis-ci.org/kbrebanov/ansible-grafana)

This role requires Ansible 1.9 or higher.

Role Variables
--------------

| Name                                            | Default                                                                                                                                                           | Description                                                         |
|-------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|
| grafana_version                                 | 2.6.0                                                                                                                                                             | Version of Grafana to install                                       |
| grafana_app_mode                                | production                                                                                                                                                        | Possible values: production, development                            |
| grafana_max_open_files                          | 10000                                                                                                                                                             | Max open files                                                      |
| grafana_restart_on_upgrade                      | false                                                                                                                                                             | Restart Grafana after upgrade                                       |
| grafana_server_cert_file                        | ''                                                                                                                                                                | HTTPS cert file                                                     |
| grafana_server_cert_key                         | ''                                                                                                                                                                | HTTPS key file                                                      |
| grafana_server_domain                           | localhost                                                                                                                                                         | The public facing domain name used to access grafana from a browser |
| grafana_server_enable_gzip                      | false                                                                                                                                                             | Enable gzip                                                         |
| grafana_server_enforce_domain                   | false                                                                                                                                                             | Redirect to correct domain if host header does not match domain     |
| grafana_server_http_addr                        | ''                                                                                                                                                                | The ip address to bind to, empty will bind to all interfaces        |
| grafana_server_http_port                        | 3000                                                                                                                                                              | The http port to use                                                |
| grafana_server_protocol                         | http                                                                                                                                                              | Protocol (http or https)                                            |
| grafana_server_root_url                         | "%(protocol)s://%(domain)s:%(http_port)s/"                                                                                                                        | The full public facing url                                          |
| grafana_server_router_logging                   | false                                                                                                                                                             | Log web requests                                                    |
| grafana_server_static_root_path                 | public                                                                                                                                                            | The path relative working path                                      |
| grafana_database_type                           | sqlite3                                                                                                                                                           | Database type, either "mysql", "postgres" or "sqlite3"              |
| grafana_database_host                           | 127.0.0.1:3306                                                                                                                                                    | Database host and port                                              |
| grafana_database_name                           | grafana                                                                                                                                                           | Database name                                                       |
| grafana_database_user                           | root                                                                                                                                                              | Database user                                                       |
| grafana_database_password                       | ''                                                                                                                                                                | Database password                                                   |
| grafana_database_postgres_ssl_mode              | disable                                                                                                                                                           | For "postgres" only, either "disable", "require" or "verify-full"   |
| grafana_database_sqlite3_path                   | grafana.db                                                                                                                                                        | For "sqlite3" only, path relative to data_path setting              |
| grafana_session_cookie_name                     | grafana_sess                                                                                                                                                      | Session cookie name                                                 |
| grafana_session_cookie_secure                   | false                                                                                                                                                             | If you use session in https only, default is false                  |
| grafana_session_life_time                       | 86400                                                                                                                                                             | Session life time                                                   |
| grafana_session_provider                        | file                                                                                                                                                              | Either "memory", "file", "redis", "mysql" or "postgres"             |
| grafana_session_provider_config                 | sessions                                                                                                                                                          | Provider config options                                             |
| grafana_analytics_reporting_enabled             | true                                                                                                                                                              | Sends usage counters to stats.grafana.org every 24 hours            |
| grafana_analytics_google_analytics_ua_id        | ''                                                                                                                                                                | Google Analytics universal tracking code                            |
| grafana_security_admin_user                     | admin                                                                                                                                                             | Default admin user                                                  |
| grafana_security_admin_password                 | admin                                                                                                                                                             | Default admin password                                              |
| grafana_security_cookie_remember_name           | grafana_remember                                                                                                                                                  | Name of remember cookie                                             |
| grafana_security_cookie_username                | grafana_user                                                                                                                                                      | Cookie username                                                     |
| grafana_security_data_source_proxy_whitelist    | ''                                                                                                                                                                | Data source proxy whitelist (ip_or_domain:port seperated by spaces) |
| grafana_security_disable_gravatar               | false                                                                                                                                                             | Disable Gravatar profile images                                     |
| grafana_security_login_remember_days            | 7                                                                                                                                                                 | Auto-login remember days                                            |
| grafana_security_secret_key                     | SW2YcwTIb9zpOOhoPsMm                                                                                                                                              | Used for signing                                                    |
| grafana_users_allow_org_create                  | true                                                                                                                                                              | Allow non admin users to create organizations                       |
| grafana_users_allow_sign_up                     | true                                                                                                                                                              | Disable user signup / registration                                  |
| grafana_users_auto_assign_org                   | true                                                                                                                                                              | Automatically assign new users to the default organization (id 1)   |
| grafana_users_auto_assign_org_role              | Viewer                                                                                                                                                            | Default role new users will be automatically assigned               |
| grafana_users_login_hint                        | email or username                                                                                                                                                 | Background text for the user field on the login page                |
| grafana_auth_anonymous_enabled                  | false                                                                                                                                                             | Enable anonymous access                                             |
| grafana_auth_anonymous_org_name                 | Main Org.                                                                                                                                                         | Organization name that should be used for unauthenticated users     |
| grafana_auth_anonymous_org_role                 | Viewer                                                                                                                                                            | Role for unauthenticated users                                      |
| grafana_auth_github_enabled                     | false                                                                                                                                                             | Enable GitHub authentication                                        |
| grafana_auth_github_allow_sign_up               | false                                                                                                                                                             | Allow GitHub sign up                                                |
| grafana_auth_github_client_id                   | some_id                                                                                                                                                           | GitHub client ID                                                    |
| grafana_auth_github_client_secret               | some_secret                                                                                                                                                       | GitHub client password                                              |
| grafana_auth_github_scopes                      | user:email,read:org                                                                                                                                               | GitHub scopes                                                       |
| grafana_auth_github_auth_url                    | https://github.com/login/oauth/authorize                                                                                                                          | GitHub authentication URL                                           |
| grafana_auth_github_token_url                   | https://github.com/login/oauth/access_token                                                                                                                       | GitHub token URL                                                    |
| grafana_auth_github_api_url                     | https://api.github.com/user                                                                                                                                       | GitHub API URL                                                      |
| grafana_auth_github_team_ids                    | ''                                                                                                                                                                | GitHub team ID's                                                    |
| grafana_auth_github_allowed_organizations       | ''                                                                                                                                                                | GitHub allowed organizations                                        |
| grafana_auth_google_enabled                     | false                                                                                                                                                             | Enable Google authentication                                        |
| grafana_auth_google_allow_sign_up               | false                                                                                                                                                             | Allow Google sign up                                                |
| grafana_auth_google_client_id                   | some_client_id                                                                                                                                                    | Google client ID                                                    |
| grafana_auth_google_client_secret               | some_client_secret                                                                                                                                                | Google client password                                              |
| grafana_auth_google_scopes                      | https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email                                                                   | Google scopes                                                       |
| grafana_auth_google_auth_url                    | https://accounts.google.com/o/oauth2/auth                                                                                                                         | Google authentication URL                                           |
| grafana_auth_google_token_url                   | https://accounts.google.com/o/oauth2/token                                                                                                                        | Google token URL                                                    |
| grafana_auth_google_api_url                     | https://www.googleapis.com/oauth2/v1/userinfo                                                                                                                     | Google API URL                                                      |
| grafana_auth_google_allowed_domains             | ''                                                                                                                                                                | Google allowed domains                                              |
| grafana_auth_proxy_enabled                      | false                                                                                                                                                             | Enable proxy authentication                                         |
| grafana_auth_proxy_header_name                  | X-WEBAUTH-USER                                                                                                                                                    | Proxy header name                                                   |
| grafana_auth_proxy_header_property              | username                                                                                                                                                          | Proxy header property                                               |
| grafana_auth_proxy_auto_sign_up                 | true                                                                                                                                                              | Proxy auto sign up                                                  |
| grafana_auth_basic_enabled                      | true                                                                                                                                                              | Enable basic authentication                                         |
| grafana_auth_ldap_enabled                       | false                                                                                                                                                             | Enable LDAP authentication                                          |
| grafana_auth_ldap_config_file                   | "{{ grafana_conf_dir }}/ldap.toml"                                                                                                                                | Grafana LDAP configuration file                                     |
| grafana_auth_ldap_verbose_logging               | false                                                                                                                                                             | Log user information returned from LDAP                             |
| grafana_auth_ldap_servers_host                  | 127.0.0.1                                                                                                                                                         | LDAP server host (specify multiple hosts space separated)           |
| grafana_auth_ldap_servers_port                  | 389                                                                                                                                                               | LDAP port, default is 389 or 636 if using SSL                       |
| grafana_auth_ldap_servers_use_ssl               | false                                                                                                                                                             | If LDAP server supports TLS                                         |
| grafana_auth_ldap_servers_ssl_skip_verify       | false                                                                                                                                                             | Skip LDAP SSL cert validation                                       |
| grafana_auth_ldap_servers_root_ca_cert          | ''                                                                                                                                                                | Path to your root CA certificate, unset uses system defaults        |
| grafana_auth_ldap_servers_bind_dn               | cn=admin,dc=grafana,dc=org                                                                                                                                        | Search user bind DN                                                 |
| grafana_auth_ldap_servers_bind_password         | grafana                                                                                                                                                           | Search user bind password                                           |
| grafana_auth_ldap_servers_search_filter         | "(cn=%s)"                                                                                                                                                         | User search filter                                                  |
| grafana_auth_ldap_servers_search_base_dns       | dc=grafana,dc=org                                                                                                                                                 | Base DN to search through                                           |
| grafana_auth_ldap_servers_group_search_filter   | ''                                                                                                                                                                | Group search filter                                                 |
| grafana_auth_ldap_servers_group_search_base_dns | ''                                                                                                                                                                | Base DN to search through for groups                                |
| grafana_auth_ldap_servers_attributes_name       | givenName                                                                                                                                                         | LDAP name attribute                                                 |
| grafana_auth_ldap_servers_attributes_surname    | sn                                                                                                                                                                | LDAP surname attribute                                              |
| grafana_auth_ldap_servers_attributes_username   | cn                                                                                                                                                                | LDAP username attribute                                             |
| grafana_auth_ldap_servers_attributes_member_of  | memberOf                                                                                                                                                          | LDAP member_of attribute                                            |
| grafana_auth_ldap_servers_attributes_email      | email                                                                                                                                                             | LDAP email attribute                                                |
| grafana_auth_ldap_servers_group_mappings        | [{group_dn: "cn=admins,dc=grafana,dc=org", org_role: "Admin"}, {group_dn: "cn=users,dc=grafana,dc=org", org_role: "Editor"}, {group_dn: "*", org_role: "Viewer"}] | Map LDAP groups to Grafana org roles                                |
| grafana_smtp_enabled                            | false                                                                                                                                                             | Enable SMTP                                                         |
| grafana_smtp_host                               | localhost:25                                                                                                                                                      | SMTP host and port                                                  |
| grafana_smtp_user                               |''                                                                                                                                                                 | SMTP user                                                           |
| grafana_smtp_password                           | ''                                                                                                                                                                | SMTP password                                                       |
| grafana_smtp_cert_file                          | ''                                                                                                                                                                | SMTP TLS certificate file                                           |    
| grafana_smtp_key_file                           | ''                                                                                                                                                                | SMTP TLS key file                                                   |
| grafana_smtp_skip_verify                        | false                                                                                                                                                             | Skip SMTP TLS certificate verification                              |
| grafana_smtp_from_address                       | admin@grafana.localhost                                                                                                                                           | SMTP from address                                                   |
| grafana_emails_welcome_email_on_sign_up         | false                                                                                                                                                             | Send a welcome email on user sign up                                |
| grafana_log_mode                                | [console, file]                                                                                                                                                   | Logging mode either "console", "file" or both                       |
| grafana_log_buffer_len                          | 10000                                                                                                                                                             | Logging buffer length                                               |
| grafana_log_level                               | Info                                                                                                                                                              | Either "Trace", "Debug", "Info", "Warn", "Error", "Critical"        |
| grafana_log_console_level                       | ''                                                                                                                                                                | Console logging level                                               |
| grafana_log_file_level                          | ''                                                                                                                                                                | File logging level                                                  |
| grafana_log_file_log_rotate                     | true                                                                                                                                                              | Automated log rotation                                              |
| grafana_log_file_max_lines                      | 1000000                                                                                                                                                           | Max line number of single file                                      |
| grafana_log_file_max_lines_shift                | 28                                                                                                                                                                | Max size shift of single file, default is 28 means 1 << 28, 256MB   |
| grafana_log_file_daily_rotate                   | true                                                                                                                                                              | Rotate log daily                                                    |
| grafana_log_file_max_days                       | 7                                                                                                                                                                 | Expired days of log file                                            |
| grafana_event_publisher_enabled                 | false                                                                                                                                                             | Enable AMPQ event publisher                                         |
| grafana_event_publisher_rabbitmq_url            | amqp://localhost/                                                                                                                                                 | RabbitMQ URL                                                        |
| grafana_event_publisher_exchange                | grafana_events                                                                                                                                                    | RabbitMQ exchange                                                   |
| grafana_dashboards_json_enabled                 | false                                                                                                                                                             | Enable dashboard JSON files                                         |
| grafana_dashboards_json_path                    | "{{ grafana_data_dir }}/dashboards"                                                                                                                               | Dashboard JSON files path                                           |

Dependencies
------------

None

Example Playbook
----------------

Install Grafana
```
- hosts: all
  roles:
    - kbrebanov.grafana
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov