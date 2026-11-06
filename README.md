# Проект: личный VPN + мониторинг + подготовка к failover

Локальная документация и шаблоны для:

- **Oracle Cloud Always Free** — основная «мастер»-машина (2 OCPU / 12 GB RAM ARM, ~10 TB egress/мес по документации Oracle).
- **VLESS** (или иной протокол на ваш выбор) — доступ с ваших устройств.
- **Uptime Kuma** (или аналог) — внешние проверки HTTP/TCP, алерты.
- **Failover между провайдерами** (Reg.ru → Yandex Cloud и т.д.) — через **IaC + DNS**, а не «ручной клон диска».

Подробный пошаговый план: [docs/RUNBOOK.md](./docs/RUNBOOK.md).

## Быстрый старт

1. Прочитать [RUNBOOK.md](./docs/RUNBOOK.md) и выписать свои домены, регионы, типы деплоя.
2. Создать репозиторий на GitHub (см. раздел ниже) и запушить эту папку.
3. Дальше — по фазам в RUNBOOK (Oracle → мониторинг → упаковка приложений → автоматизация failover).

## Создать репозиторий на GitHub

**Вариант A — через веб-интерфейс**

1. На https://github.com/new создайте репозиторий (например `SAURON`), **без** README (чтобы не конфликтовал с локальным).
2. В папке проекта выполните:

```bash
cd D:/DEV/SAURON
git init
git add .
git commit -m "Initial runbook and structure"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/SAURON.git
git push -u origin main
```

**Вариант B — через GitHub CLI**

```bash
gh auth login
cd D:/DEV/SAURON
git init
git add .
git commit -m "Initial runbook and structure"
gh repo create YOUR_USERNAME/SAURON --public --source=. --remote=origin --push
```

## Структура репозитория

| Путь | Назначение |
|------|------------|
| `docs/RUNBOOK.md` | Полный сценарий по фазам |
| `templates/` | Заготовки под ваши Terraform/Ansible (добавляете сами) |

## Важно

- Условия использования облаков (в т.ч. Oracle) и допустимость VPN — **проверьте в актуальной оферте** провайдера.
- **Не коммитьте** API-ключи, `.env` с секретами, приватные ключи — используйте переменные окружения и секрет-хранилища провайдера.

## Лицензия

Документация для личного использования — при необходимости добавьте `LICENSE` по своему усмотрению.
