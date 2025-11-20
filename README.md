# ansible-whoami-deploy

Proyecto de ejemplo de **DevOps / Infra ligera** con:

- Ansible
- Docker / Docker Compose
- Nginx como reverse proxy
- Variables centralizadas en `group_vars`

El objetivo es desplegar un servicio `whoami` en Docker y publicarlo a través de Nginx
de forma reproducible, sin tener que conectarse por SSH ni ejecutar comandos manualmente.

## Estructura

```text
ansible-whoami-deploy/
├─ ansible.cfg
├─ inventory
├─ deploy.yml
├─ group_vars/
│  └─ all.yml
└─ roles/
   ├─ docker/
   │  └─ tasks/main.yml
   ├─ whoami/
   │  ├─ tasks/main.yml
   │  └─ templates/docker-compose.yml.j2
   └─ nginx/
      ├─ tasks/main.yml
      └─ templates/nginx-whoami.conf.j2
```

## Uso rápido

1. Clona el repositorio:

```bash
git clone https://github.com/jpavonabian/ansible-whoami-deploy.git
cd ansible-whoami-deploy
```

2. Edita el archivo `inventory` y ajusta el host destino (por defecto `localhost`).

3. Opcionalmente, ajusta variables en `group_vars/all.yml`:

- `whoami_host_port`
- `whoami_deploy_path`
- `whoami_server_name`

4. Ejecuta el playbook:

```bash
ansible-playbook deploy.yml
```

5. Prueba en el navegador o con curl:

```bash
curl http://TU_HOST/
```

Deberías ver la respuesta del servicio whoami servida a través de Nginx.
