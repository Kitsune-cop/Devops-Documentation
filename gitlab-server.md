# Install gitlab server

```
cd cd /home/<user>
```

- install docker

```
sudo snap install docker --classic
```

- create folder gitlab

```
sudo mkdir gitlab
```
- gitlab version list : [https://gitlab-com.gitlab.io/support/toolbox/upgrade-path/](https://gitlab-com.gitlab.io/support/toolbox/upgrade-path/)
- create file `/home/<user>/gitlab/docker-compose.yml`

```
services:
  gitlab:
    image: gitlab/gitlab-ce:18.6.2-ce.0
    container_name: gitlab
    restart: always
    hostname: '<gitlab-domain-name>'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        # Add any other gitlab.rb configuration here, each on its own line
        external_url '<gitlab-url>'
        registry_external_url '<registry-url>'
        letsencrypt['enable'] = false
    ports:
      - '80:80'
      - '443:443'
      - '8022:22'
    volumes:
      - '/home/<user>/gitlab/config:/etc/gitlab'
      - '/home/<user>/gitlab/logs:/var/log/gitlab'
      - '/home/<user>/gitlab/data:/var/opt/gitlab'
      - '/home/<user>/gitlab/ssl:/etc/gitlab/ssl'
    shm_size: '256m'
```

> copy content from other server

- `file /home/<user>/gitlab/ssl/<gitlab-domain-name>.crt`
- `file /home/<user>/gitlab/ssl/<gitlab-domain-name>.key`
- `file /home/<user>/gitlab/ssl/<registry-domain-name>.crt`
- `file /home/<user>/gitlab/ssl/<registry-domain-name>.key`

> start server

```
sudo docker compose up -d
```

> Log in as admin
> go to setting -> CI/CD -> Continuos Integration Deployment -> uncheck default to auto Devops,