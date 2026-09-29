# Docker-порт StaticJinjaPlus

Набор Dockerfile'ов для сборки образов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus).

## Файлы

### Универсальные (порт)
Позволяют собрать любую версию через `--build-arg APP_VERSION`.
- `Dockerfile.ubuntu` — база Ubuntu
- `Dockerfile.slim` — база python-slim

### Архивные релизы
Собирают конкретную версию с проверкой контрольной суммы (`--checksum`).
- `Dockerfile.arch010` — версия 0.1.0, Ubuntu
- `Dockerfile.slim010` — версия 0.1.0, python-slim
- `Dockerfile.arch011` — версия 0.1.1, Ubuntu
- `Dockerfile.slim011` — версия 0.1.1, python-slim

### Dev-версии
Собирают последний коммит из main-ветки. Без `--checksum`, так как содержимое
архива меняется при каждом коммите.
- `Dockerfile.dev` — main, Ubuntu
- `Dockerfile.dev-slim` — main, python-slim

## Сборка

### Универсальные (порт)

Последний main:
    
    docker build -f Dockerfile.ubuntu -t static-jinja-plus:develop .
    docker build -f Dockerfile.slim   -t static-jinja-plus:develop-slim .

Конкретная версия:
    
    docker build -f Dockerfile.ubuntu --build-arg APP_VERSION=0.1.1 -t static-jinja-plus:latest .
    docker build -f Dockerfile.slim   --build-arg APP_VERSION=0.1.1 -t static-jinja-plus:slim .

### Архивные релизы

    docker build -f Dockerfile.arch010 -t static-jinja-plus:0.1.0 .
    docker build -f Dockerfile.slim010 -t static-jinja-plus:0.1.0-slim .
    docker build -f Dockerfile.arch011 -t static-jinja-plus:0.1.1 .
    docker build -f Dockerfile.slim011 -t static-jinja-plus:0.1.1-slim .

### Dev-версии

    docker build -f Dockerfile.dev      -t static-jinja-plus:develop .
    docker build -f Dockerfile.dev-slim -t static-jinja-plus:develop-slim .

## Запуск

    docker run --rm static-jinja-plus:<тег>

Приложение рендерит HTML-файлы из шаблонов и завершает работу.

Все собранные образы доступны по адресу:
https://hub.docker.com/r/skripbug/static-jinja-plus
