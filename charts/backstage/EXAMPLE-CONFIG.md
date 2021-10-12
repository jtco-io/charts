# Example app-config.yaml

Rather than setting these values in your docker image we pass them into a configmap automatically rolling your helm 
release's pods anytime you change these values.

See the [Backstage docs](https://backstage.io/docs/conf/writing#file-format) for more information.

```yaml
  app:
    title: Scaffolded Backstage App
    baseUrl: https://backstage.mydomain.com

  organization:
    name: MY ORG

  backend:
    baseUrl: https://backstage.mydomain.com
    listen:
      port: 7000
    csp:
      connect-src: ["'self'", 'http:', 'https:']
      # Content-Security-Policy directives follow the Helmet format: https://helmetjs.github.io/#reference
      # Default Helmet Content-Security-Policy values can be removed by setting the key to false
    cors:
      origin: http://backstage.mydomain.com
      methods: [GET, POST, PUT, DELETE]
      credentials: true
    # config options: https://node-postgres.com/api/client
    database:
      client: pg
      connection:
        host: ${POSTGRES_HOST}
        port: ${POSTGRES_PORT}
        user: ${POSTGRES_USER}
        password: ${POSTGRES_PASSWORD}
        database: ${POSTGRES_DATABASE}
        # https://node-postgres.com/features/ssl
        # ssl: require # see https://www.postgresql.org/docs/current/libpq-ssl.html Table 33.1. SSL Mode Descriptions (e.g. require)
        #   ca: # if you have a CA file and want to verify it you can uncomment this section
        #     $file: <file-path>/ca/server.crt
    cache:
      store: memory
    # workingDirectory: /tmp # Use this to configure a working directory for the scaffolder, defaults to the OS temp-dir

  integrations:
    gitlab:
      - host: gitlab.com
        token: ${GITLAB_TOKEN}
      ### Example for how to add your GitHub Enterprise instance using the API:
      # - host: ghe.example.net
      #   apiBaseUrl: https://ghe.example.net/api/v3
      #   token: ${GHE_TOKEN}

  proxy:
    '/test':
      target: 'https://example.com'
      changeOrigin: true

  # Reference documentation http://backstage.io/docs/features/techdocs/configuration
  # Note: After experimenting with basic setup, use CI/CD to generate docs
  # and an external cloud storage when deploying TechDocs for production use-case.
  # https://backstage.io/docs/features/techdocs/how-to-guides#how-to-migrate-from-techdocs-basic-to-recommended-deployment-approach
  techdocs:
    builder: 'local' # Alternatives - 'external'
    generator:
      runIn: 'docker' # Alternatives - 'local'
    publisher:
      type: 'local' # Alternatives - 'googleGcs' or 'awsS3'. Read documentation for using alternatives.

  auth:
    # see https://backstage.io/docs/auth/ to learn about auth providers
    providers: {}

  scaffolder:
    github:
      token: ${GITHUB_TOKEN}
      visibility: public # or 'internal' or 'private'

  catalog:
    rules:
      - allow: [Component, System, API, Group, User, Resource, Location]
    locations: []
```
