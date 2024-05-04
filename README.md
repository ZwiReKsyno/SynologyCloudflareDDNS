# Скрипт Synology Cloudflare DDNS  📜

Это сценарий, который можно использовать для добавления [Cloudflare](https://www.cloudflare.com/) в качестве DDNS к [Synology](https://www.synology.com/)  NAS. В скрипте использовался обновленный API Cloudflare API v4.

## Как использовать

### Доступ к Synology через SSH

1. Войдите в свой DSM
2. Перейдите в Панель управления > Терминал и SNMP > Включить службу SSH.
3. Используйте свой клиент для доступа к Synology через SSH.
4. Для подключения используйте свою учетную запись администратора Synology.

### Запуск команд в Synology

1. Загрузите cloudflareddns.shиз этого репозитория/sbin/cloudflareddns.sh

```
wget https://raw.githubusercontent.com/joshuaavalon/SynologyCloudflareDDNS/master/cloudflareddns.sh -O /sbin/cloudflareddns.sh
```

Это не обязательно, вы можете указать все, что захотите. Если вы поместите скрипт под другое имя или путь, убедитесь, что вы используете правильный путь.

2. Дайте другим разрешение на выполнение

```
chmod +x /sbin/cloudflareddns.sh
```

3. Добавить cloudflareddns.shв Synology

```
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare]
        modulepath=/sbin/cloudflareddns.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
E*.
```

queryurl не имеет значения, потому что мы собираемся использовать наш скрипт, но он необходим.

### Получить параметры Cloudflare

1. Перейдите на страницу обзора своего домена и скопируйте идентификатор своей зоны.
2. Перейдите в свой профиль > Токены API > Создать токен . Он должен иметь разрешения Zone > DNS > Edit. Скопируйте токен API.

### Настройка ДДНС

1. Войдите в свой DSM
2. Перейдите в Панель управления > Внешний доступ > DDNS > Добавить.
3. Введите следующее:
   - Поставщик услуг:Cloudflare
   - Имя хоста:www.example.com
   - Имя пользователя/электронная почта:<Zone ID>
   - Ключ пароля:<API Token>
