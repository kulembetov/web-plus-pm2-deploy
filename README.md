# Деплой приложения с использованием PM2

Этот README описывает процесс автоматизации деплоя фронтенда и бэкенда при помощи PM2. Мы будем использовать PM2 Deploy для управления приложением на удаленном сервере.

## IP-адрес сервера:
158.160.40.178

## Frontend:
https://mesto.kulembetov.nomoredomainsmonster.ru

## Backend:
https://api.mesto.kulembetov.nomoredomainsmonster.ru

## Шаг 1: Установка PM2
Если PM2 не установлен на вашем сервере, установите его с помощью следующей команды:

```bash
npm install pm2 -g
```

## Шаг 2: Настройка проекта
Создайте конфигурационные файлы для фронтенда и бэкенда:

## Пример файла конфигурации для фронтенда
```
module.exports = {
  apps : [{
    name: 'frontend',
    script: 'npm',
    args: 'start',
    env: {
      NODE_ENV: 'production',
      PORT: 80
    }
  }],
  deploy : {
    production : {
      user : 'username',
      host : '158.160.40.178',
      ref  : 'origin/main',
      repo : 'git@github.com:username/frontend-repo.git',
      path : '/var/www/frontend',
      'post-deploy' : 'npm install && npm run build && pm2 reload all'
    }
  }
};
```

## Пример файла конфигурации для бэкенда
```
module.exports = {
  apps : [{
    name: 'backend',
    script: 'npm',
    args: 'start',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }],
  deploy : {
    production : {
      user : 'username',
      host : '158.160.40.178',
      ref  : 'origin/main',
      repo : 'git@github.com:username/backend-repo.git',
      path : '/var/www/backend',
      'post-deploy' : 'npm install && pm2 reload all'
    }
  }
};
```

### Шаг 3: Деплой
Запустите процесс деплоя для фронтенда и бэкенда с помощью команды PM2 Deploy
```
pm2 deploy ecosystem.config.js production
```

Это автоматически клонирует репозиторий, устанавливает зависимости, выполняет сборку (для фронтенда) и перезапускает приложение с использованием PM2.

### Теперь ваше приложение доступно по следующим URL-адресам:

## Фронтенд: https://mesto.kulembetov.nomoredomainsmonster.ru

## Бэкенд: https://api.mesto.kulembetov.nomoredomainsmonster.ru

### Шаг 4: Управление приложением
Вы можете управлять вашим приложением с помощью PM2 команд, например:

```v
## Запуск приложения: pm2 start app_name

## Остановка приложения: pm2 stop app_name'

## Перезапуск приложения: pm2 restart app_name
```
Готово! Теперь у вас есть автоматизированный процесс деплоя приложения с использованием PM2 на вашем удаленном сервере.

## Лицензия

Проект распространяется под [MIT License](https://github.com/kulembetov/web-plus-pm2-deploy/blob/main/MIT-LICENSE.md),  которая является свободной и краткой. Она позволяет людям делать с вашим кодом всё, что они хотят, включая использование его в коммерческих и промо-подобных проектах.
