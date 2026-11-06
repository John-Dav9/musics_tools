# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Instruments de musique": a Symfony 7.4 web app (PHP >= 8.2) in early stage, basically the Flex skeleton with no entities, controllers or tests yet. Repo: https://github.com/John-Dav9/musics_tools. The README and the domain are in French. Development runs under WSL on Windows 11.

`install.sh` at the root is the Claude Code installer script. It is not part of the app.

## Commands

```bash
composer install                      # also runs cache:clear, assets:install, importmap:install
docker compose up -d                  # Postgres 16 (+ Mailpit via compose.override.yaml)
symfony serve -d                      # dev server (Symfony CLI is installed)
php bin/console doctrine:migrations:migrate
php bin/console make:entity           # maker-bundle: entities, controllers, forms, tests
php bin/console make:migration

php bin/phpunit                       # all tests (APP_ENV=test)
php bin/phpunit tests/Path/To/SomeTest.php
php bin/phpunit --filter testMethodName
```

PHPUnit is configured with `failOnDeprecation`, `failOnNotice` and `failOnWarning`, so a deprecation fails the build. The test DB name gets a `_test` suffix (from `config/packages/doctrine.yaml`).

## Architecture

- **Backend**: standard Symfony layout. Doctrine ORM 3 with **attribute mappings** in `src/Entity` (`App\Entity`), repositories in `src/Repository`, controllers in `src/Controller` using attribute routes. Services are autowired from `config/services.yaml`.
- **Database**: PostgreSQL 16 (`DATABASE_URL` in `.env`; put local overrides in `.env.local`, which is gitignored). Identity columns are used for IDs on Postgres.
- **Frontend**: AssetMapper + importmap (`importmap.php`). There is no Node/webpack build. JS entry is `assets/app.js`, styles are in `assets/styles/`. Stimulus controllers live in `assets/controllers/` and Turbo is enabled (Symfony UX). Templates extend `templates/base.html.twig`.
- **Messenger**: emails (`SendEmailMessage`), chat and SMS notifications are routed to the `async` Doctrine transport, so a worker (`php bin/console messenger:consume async`) has to run for them to be sent. Failed messages go to the `failed` transport.
- **Security**: the bundle is installed, but it uses a placeholder `users_in_memory` provider until a User entity exists.

## Repo notes

- `vendor/` is listed in `.gitignore`, but it was committed in the initial commit, so changes under it still show up in `git status`. Don't commit vendor changes. Ask before untracking it.
