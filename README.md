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

## Фронтенд
```module.exports = {
  apps: [
    {
      name: 'frontend',
      script: 'path/to/your/frontend/app.js',
      env: {
        NODE_ENV: 'production',
        PORT: 80,
      },
    },
  ],
  deploy: {
    production: {
      user: 'your-ssh-username',
      host: '158.160.40.178',
      ref: 'origin/main',
      repo: 'git@github.com:your-username/your-frontend-repo.git',
      path: '/path/to/your/remote/frontend/directory',
      'post-deploy': 'npm install && npm run build && pm2 reload frontend',
    },
  },
};
```

## Бэкенд
```
module.exports = {
  apps: [
    {
      name: 'backend',
      script: 'path/to/your/backend/app.js',
      env: {
        NODE_ENV: 'production',
        PORT: 3000,
      },
    },
  ],
  deploy: {
    production: {
      user: 'your-ssh-username',
      host: '158.160.40.178',
      ref: 'origin/main',
      repo: 'git@github.com:your-username/your-backend-repo.git',
      path: '/path/to/your/remote/backend/directory',
      'post-deploy': 'npm install && pm2 reload backend',
    },
  },
};
```

### Шаг 3: Деплой
Запустите деплой для фронтенда и бэкенда с помощью PM2 Deploy

## Для фронтенда
```
pm2 deploy frontend production
```

## Для бэкенда
```
pm2 deploy backend production
```

Это автоматически клонирует репозиторий, устанавливает зависимости, выполняет сборку (для фронтенда) и перезапускает приложение с использованием PM2.

## Теперь ваше приложение доступно по следующим URL-адресам:

### Фронтенд: https://mesto.kulembetov.nomoredomainsmonster.ru

### Бэкенд: https://api.mesto.kulembetov.nomoredomainsmonster.ru

### Шаг 4: Управление приложением

Вы можете управлять вашим приложением с помощью PM2 команд, например:

```
## Запуск приложения:
pm2 start app_name

## Остановка приложения: pm2 stop app_name'

## Перезапуск приложения: pm2 restart app_name
```
Готово! Теперь у вас есть автоматизированный процесс деплоя приложения с использованием PM2 на вашем удаленном сервере.

## License

The [MIT License](https://github.com/kulembetov/web-plus-pm2-deploy/blob/main/README.md) is a permissive license that is short and to the point. It lets people do anything they want with your code as long as they provide attribution back to you and don’t hold you liable.
