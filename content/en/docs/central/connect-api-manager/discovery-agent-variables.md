---
title: Discovery Agent variables
linkTitle: Discovery Agent variables
draft: true
weight: 40
description: >-
  
  Use the following environment variables to create your Discovery Agent env_vars file. for additional information, see Deploy your agents.
---

| Variable name                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |   |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
| API Manager variables                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |   |
| APIMANAGER_HOST                         | The host API Manager is running on (localhost).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |   |
| APIMANAGER_PORT                         | The port API Manager is listening on.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |   |
| APIMANAGER_DISCOVERYIGNORETAGS          | Comma-separated blacklist of tags that should not be on a Proxy before sending to AMPLIFY Central. Take precedence over APIMANAGER_FILTER                                                                                                                                                                                                                                                                                                                                                                                               |   |
| APIMANAGER_FILTER                       | Expression to filter the API you want the agent to discover. See Filtering APIs to be discovered for conditional expression samples.                                                                                                                                                                                                                                                                                                                                                                                                    |   |
| APIMANAGER_APIVERSION                   | The API version of the API Manager (1.3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |   |
| APIMANAGER_POLLINTERVAL                 | The frequency in which API Manager is polled for new endpoints (default=ns, us, ms, s, m, h). Set to 30s.                                                                                                                                                                                                                                                                                                                                                                                                                               |   |
| APIMANAGER_PROXYAPICIDFIELD             | The field name used to store AMPLIFY Central identifier for the frontend proxy in API Manager.                                                                                                                                                                                                                                                                                                                                                                                                                                          |   |
| APIMANAGER_PROXYURL                     | The URL for the proxy for API Manager <http://username:password@hostname:port>. If empty, no proxy is defined.                                                                                                                                                                                                                                                                                                                                                                                                                          |   |
| APIMANAGER_SUBSCRIPTIONAPPLICATIONFIELD | The field name used to save subscription IDs to the API Manager application (default=subscriptions). To display this in the UI, add a custom property under applications in your API Manager configuration. See Customize API Manager.                                                                                                                                                                                                                                                                                                  |   |
| APIMANAGER_AUTH_USERNAME                | The API Manager username for this agent. Created in API Manager (must be API Manager Admin).                                                                                                                                                                                                                                                                                                                                                                                                                                            |   |
| APIMANAGER_AUTH_PASSWORD                | The password created for the API Manager username created for this agent (created in API Manager).                                                                                                                                                                                                                                                                                                                                                                                                                                      |   |
| APIMANAGER_SSL_MINVERSION               | String value for the minimum SSL/TLS version that is acceptable. If zero, empty TLS 1.0 is taken as the minimum. Allowed values are: TLS1.0, TLS1.1, TLS1.2, TLS1.3.                                                                                                                                                                                                                                                                                                                                                                    |   |
| APIMANAGER_SSL_MAXVERSION               | String value for the maximum SSL/TLS version that is acceptable. If empty, then the maximum version supported by this package is used, which is currently TLS 1.3. Allowed values are: TLS1.0, TLS1.1, TLS1.2, TLS1.3.                                                                                                                                                                                                                                                                                                                  |   |
| APIMANAGER_SSL_CIPHERSUITES             | An array of strings. It is a list of supported cipher suites for TLS versions up to TLS 1.2. If CipherSuites is nil, a default list of secure cipher suites is used, with a preference order based on hardware performance. See Supported Cipher Suites.                                                                                                                                                                                                                                                                                |   |
| APIMANAGER_SSL_NEXTPROTOS               | An array of strings. It is a list of supported application level protocols, in order of preference, based on the ALPN protocol list. Allowed values are: h2, http/1.0, http/1.1, h2c.                                                                                                                                                                                                                                                                                                                                                   |   |
| APIMANAGER_SSL_INSECURESKIPVERIFY       | Controls whether a client verifies the server's certificate chain and host name. If true, TLS accepts any certificate presented by the server and any host name in that certificate. In this mode, TLS is susceptible to man-in-the-middle attacks.                                                                                                                                                                                                                                                                                     |   |
| LOG_LEVEL                               | The log level for output messages (debug, info, warn, error).                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |   |
| LOG_FORMAT                              | The format to print log messages (json, line, package).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |   |
| LOG_OUTPUT                              | The output for the log lines (stdout, file, both).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |   |
| LOG_PATH                                | The path (relative or absolute) to save logs files, if output type file or both.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |   |
| AMPLIFY Central variables               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |   |
| CENTRAL_URL                             | The URL to the AMPLIFY Central instance being used for this Discovery Agent.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |   |
| CENTRAL_TENANTID                        | The Organization ID from AMPLIFY Central. Locate this at Platform > User > Organization.                                                                                                                                                                                                                                                                                                                                                                                                                                                |   |
| CENTRAL_TEAMID                          | The Team ID in AMPLIFY Central that all AWS APIs will be linked. Locate this at AMPLIFY Central > Access > Teams.                                                                                                                                                                                                                                                                                                                                                                                                                       |   |
| CENTRAL_MODE                            | Method to send endpoints back to Central. (connected = API Server, disconnected = Catalog).                                                                                                                                                                                                                                                                                                                                                                                                                                             |   |
| CENTRAL_PROXYURL                        | The URL for the proxy for Amplify Central <http://username:password@hostname:port>. If empty, no proxy is defined.                                                                                                                                                                                                                                                                                                                                                                                                                      |   |
| CENTRAL_ENVIRONMENT                     | Environment that is set by download kit in APIC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |   |
| CENTRAL_AUTH_URL                        | The AMPLIFY login URL: <https://login.axway.com/auth>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |   |
| CENTRAL_AUTH_REALM                      | The Realm used to authenticate for AMPLIFY Central.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |   |
| CENTRAL_AUTH_CLIENTID                   | The name of the Service Account created in AMPLIFY Central. Locate this at AMPLIFY Central > Access > Service Accounts.                                                                                                                                                                                                                                                                                                                                                                                                                 |   |
| CENTRAL_AUTH_PRIVATEKEY                 | The private key associated with the Service Account.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |   |
| CENTRAL_AUTH_PUBLICKEY                  | The public key associated to the Service Account. Extract using the following commands:openssl genpkey -algorithm RSA -out ./private_key.pem -pkeyopt rsa_keygen_bits:2048openssl rsa -pubout -in ./private_key.pem -out ./public_key.pemopenssl rsa -pubout -in ./private_key.pem -out ./public_key.der -outform derbase64 ./public_key.der > ./public_keyIf the keys for APIC service account have already been generated, then only the 3rd and 4th bullet points need to be run using the public key that was previously generated. |   |
| CENTRAL_AUTH_KEYPASSWORD                | The password for the private key, if applicable.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |   |
| CENTRAL_AUTH_TIMEOUT                    | The timeout to wait for the authentication server to respond (ns - default, us, ms, s, m, h). Set to 10s.                                                                                                                                                                                                                                                                                                                                                                                                                               |   |
| CENTRAL_ENVIRONMENT                     | Name of the AMPLIFY Central environment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |   |
| CENTRAL_APISERVERVERSION                | Version of the API Server that the agent will communicate with                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |   |
| CENTRAL_ADDITIONALTAGS                  | Additional tag names to publish separated by a comma.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |   |
| CENTRAL_SSL_MINVERSION                  | String value for the minimum SSL/TLS version that is acceptable. If zero, empty TLS 1.0 is taken as the minimum. Allowed values are: TLS1.0, TLS1.1, TLS1.2, TLS1.3.                                                                                                                                                                                                                                                                                                                                                                    |   |
| CENTRAL_SSL_MAXVERSION                  | String value for the maximum SSL/TLS version that is acceptable. If empty, then the maximum version supported by this package is used, which is currently TLS 1.3. Allowed values are: TLS1.0, TLS1.1, TLS1.2, TLS1.3.                                                                                                                                                                                                                                                                                                                  |   |
| CENTRAL_SSL_CIPHERSUITES                | An array of strings. It is a list of supported cipher suites for TLS versions up to TLS 1.2. If CipherSuites is nil, a default list of secure cipher suites is used, with a preference order based on hardware performance. See Supported Cipher Suites.                                                                                                                                                                                                                                                                                |   |
| CENTRAL_SSL_NEXTPROTOS                  | An array of strings. It is a list of supported application level protocols, in order of preference, based on the ALPN protocol list. Allowed values are: h2, http/1.0, http/1.1, h2c.                                                                                                                                                                                                                                                                                                                                                   |   |
| CENTRAL_SSL_INSECURESKIPVERIFY          | Controls whether a client verifies the server's certificate chain and host name. If true, TLS accepts any certificate presented by the server and any host name in that certificate. In this mode, TLS is susceptible to man-in-the-middle attacks.                                                                                                                                                                                                                                                                                     |   |