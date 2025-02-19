# xray-vps-setup
VLESS со своим доменом. А что еще нужно для счастья?  

В данном варианте VLESS слушает на 443 и принимате все запросы, делая запрос на локальный Caddy только для сертификатов. В таком варианте задержка будет меньше, чем в варианте с Caddy/NGINX перед VLESS, где происходит множество лишних запросов. 
## Скрипт

- Установит Xray/Marzban на ваш выбор. Для маскировки страницы используется [Conflunce](https://github.com/Jolymmiles/confluence-marzban-home)
- На ваше усмотрение настроит:
- - Iptables, запретив все подключения, кроме SSH, 80 и 443.
- - Создаст пользователя для подключения, запретив вход от рута
- - Добавит этому пользователю ключ для SSH, запретив вход по паролю
- Настроит WARP для ру-сайтов.  
```bash
bash <(wget -qO- https://raw.githubusercontent.com/Kokoc-tech/xray-vps-setup/refs/heads/main/vps-setup.sh)
```

## Плейбук

[Ansible-galaxy](https://galaxy.ansible.com/ui/standalone/roles/Kokoc-tech/xray-vps-setup/install/)
```yaml
- name: Setup vps 
  hosts: some_host
  roles:
    - Kokoc-tech.xray-vps-setup  
  vars:
    domain: example.com # домен, уровень неважен
    setup_variant: marzban # marzban or xray
    setup_warp: false # true or false
    configure_security: true # true or false
    user_to_create: xray_user # если configure_security: true, то обязательно
    user_password: "xray_password" # если configure_security: true, то обязательно
    SSH_PORT: 22 # если configure_security: true, то обязательно
    ssh_public_key: "" # если configure_security: true, то обязательно
```

## Ручная установка

Описана [здесь](https://github.com/Kokoc-tech/xray-vps-setup/blob/main/install_in_docker.md).  

## Почему не nginx, haproxy, 3x-ui, x-ui, sing-box...

Caddy сам получит сертификаты, поэтому нам не придется их получать через `acme.sh` или `certbot`.  
3X-ui мерзотная панель.  
Sing-box не очень.  
XHTTP позже, а больше не надо. Уже точно. 

## Связь
Issues, PR ну или мой [тг](https://t.me/Kokoc-tech).

> [!IMPORTANT]
> Дайте секс
