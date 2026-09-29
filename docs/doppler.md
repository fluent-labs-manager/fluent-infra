# Работа с конфигурациями в Doppler

## Назначение

Проект фронтенда в Doppler: `fluent-frontend`.

| Сценарий                  | Конфиг Doppler | GitHub Environment |
|---------------------------|----------------|--------------------|
| Локальная разработка      | `dev`          | —                  |
| Проверки CI и PR-сборки   | `ci`           | `ci`               |
| Сборка и деплой из `main` | `prd`          | `production`       |

## Локальная разработка

1. Установите [Doppler CLI](https://docs.doppler.com/docs/install-cli).
2. Войдите в свой аккаунт: `doppler login`.
3. В корне `fluent-frontend` запускайте приложение через Doppler:

   ```bash
   doppler run -- npm run dev
   ```

   Файл `doppler.yaml` связывает этот каталог с проектом `fluent-frontend` и
   конфигом `dev`. Для разового запуска другого конфига укажите его явно:

   ```bash
   doppler run --project fluent-frontend --config ci -- npm run test:unit:ci
   ```

Не копируйте значения из Doppler в `.env*`. При необходимости добавить или
изменить значение используйте интерфейс Doppler и согласуйте изменение с
командой.

## Переменные фронтенда

Клиентский код получает переменные Vite через `import.meta.env`. Поэтому
используйте префикс `VITE_`, например `VITE_API_URL`,
`VITE_API_SOCKET_URL` и `VITE_SENTRY_DSN_URL`.

Значения `VITE_*` встраиваются в собранный JavaScript и доступны пользователю
в браузере. В них нельзя хранить пароли, токены доступа, приватные ключи и
другие секреты. API URL и Sentry DSN — допустимые примеры публичной
конфигурации.

`SENTRY_AUTH_TOKEN` не имеет префикса `VITE_`: он нужен только во время
release-сборки для загрузки sourcemaps и не должен попадать в бандл.

## CI/CD и GitHub

Конфиги `ci` и `prd` синхронизируются из Doppler в GitHub Environment secrets, так что при изменении данных в Doppler
менять их вручную в GitHub не нужно.
