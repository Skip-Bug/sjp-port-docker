# Docker-порт StaticJinjaPlus

Набор Dockerfile'ов для сборки образов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus).
Исходники приложения в этом репозитории **не хранятся** — каждый Dockerfile
скачивает нужную версию с GitHub в момент сборки.

## Файлы

### Универсальные (порт)
Позволяют собрать любую версию через `--build-arg APP_VERSION`
и сменить базовый образ через `--build-arg BASE_IMAGE`.
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

```bash
docker build -f Dockerfile.ubuntu -t static-jinja-plus:develop .
docker build -f Dockerfile.slim   -t static-jinja-plus:develop-slim .
```

Конкретная версия:

```bash
docker build -f Dockerfile.ubuntu --build-arg APP_VERSION=0.1.1 -t static-jinja-plus:latest .
docker build -f Dockerfile.slim   --build-arg APP_VERSION=0.1.1 -t static-jinja-plus:slim .
```

Замена базового образа:

По умолчанию:
- `Dockerfile.ubuntu` → `ubuntu:24.04`
- `Dockerfile.slim` → `python:3.12.14-slim-bookworm`

```bash
# Ubuntu 22.04 вместо 24.04
docker build -f Dockerfile.ubuntu \
  --build-arg BASE_IMAGE=ubuntu:22.04 \
  -t static-jinja-plus:test .

# Другая версия python-slim
docker build -f Dockerfile.slim \
  --build-arg BASE_IMAGE=python:3.11-slim-bookworm \
  -t static-jinja-plus:test-slim .
```

Комбинирование с версией приложения:

```bash
docker build -f Dockerfile.ubuntu \
  --build-arg BASE_IMAGE=ubuntu:22.04 \
  --build-arg APP_VERSION=0.1.1 \
  -t static-jinja-plus:0.1.1-ubuntu22 .
```

### Архивные релизы

```bash
docker build -f Dockerfile.arch010 -t static-jinja-plus:0.1.0 .
docker build -f Dockerfile.slim010 -t static-jinja-plus:0.1.0-slim .
docker build -f Dockerfile.arch011 -t static-jinja-plus:0.1.1 .
docker build -f Dockerfile.slim011 -t static-jinja-plus:0.1.1-slim .
```

### Dev-версии

```bash
docker build -f Dockerfile.dev      -t static-jinja-plus:develop .
docker build -f Dockerfile.dev-slim -t static-jinja-plus:develop-slim .
```

## Запуск

```bash
docker run --rm static-jinja-plus:<тег>
```

Приложение рендерит HTML-файлы из шаблонов и завершает работу.

## Образы на Docker Hub

Все собранные образы доступны по адресу:
https://hub.docker.com/r/skripbug/static-jinja-plus
