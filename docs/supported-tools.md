# Поддерживаемые инструменты

OpenSpec работает более чем с 20 ИИ-ассистентами для программирования. При запуске `openspec init` вам будет предложено выбрать инструменты, которые вы используете, и OpenSpec настроит соответствующие интеграции.

## Как это работает

Для каждого выбранного инструмента OpenSpec устанавливает:

1. **Навыки (Skills)** — файлы с инструкциями многократного использования, которые обеспечивают работу команд процесса `/opsx:*`.
2. **Команды (Commands)** — привязки слеш-команд, специфичные для каждого инструмента.

## Справочник директорий инструментов

| Инструмент | Расположение навыков | Расположение команд |
|------|-----------------|-------------------|
| Amazon Q Developer | `.amazonq/skills/` | `.amazonq/prompts/` |
| Antigravity | `.agent/skills/` | `.agent/workflows/` |
| Auggie (Augment CLI) | `.augment/skills/` | `.augment/commands/` |
| Claude Code | `.claude/skills/` | `.claude/commands/opsx/` |
| Cline | `.cline/skills/` | `.clinerules/workflows/` |
| CodeBuddy | `.codebuddy/skills/` | `.codebuddy/commands/opsx/` |
| Codex | `.codex/skills/` | `~/.codex/prompts/`* |
| Continue | `.continue/skills/` | `.continue/prompts/` |
| CoStrict | `.cospec/skills/` | `.cospec/openspec/commands/` |
| Crush | `.crush/skills/` | `.crush/commands/opsx/` |
| Cursor | `.cursor/skills/` | `.cursor/commands/` |
| Factory Droid | `.factory/skills/` | `.factory/commands/` |
| Gemini CLI | `.gemini/skills/` | `.gemini/commands/opsx/` |
| GitHub Copilot | `.github/skills/` | `.github/prompts/` |
| iFlow | `.iflow/skills/` | `.iflow/commands/` |
| Kilo Code | `.kilocode/skills/` | `.kilocode/workflows/` |
| OpenCode | `.opencode/skills/` | `.opencode/command/` |
| Qoder | `.qoder/skills/` | `.qoder/commands/opsx/` |
| Qwen Code | `.qwen/skills/` | `.qwen/commands/` |
| RooCode | `.roo/skills/` | `.roo/commands/` |
| Trae | `.trae/skills/` | `.trae/skills/` (через `/openspec-*`) |
| Windsurf | `.windsurf/skills/` | `.windsurf/workflows/` |

\* Команды Codex устанавливаются в глобальную домашнюю директорию (`~/.codex/prompts/` или `$CODEX_HOME/prompts/`), а не в директорию проекта.

## Неинтерактивная настройка

Для CI/CD или автоматизированной настройки используйте флаг `--tools`:

```bash
# Настроить конкретные инструменты
openspec init --tools claude,cursor

# Настроить все поддерживаемые инструменты
openspec init --tools all

# Пропустить настройку инструментов
openspec init --tools none
```

**Доступные ID инструментов:** `amazon-q`, `antigravity`, `auggie`, `claude`, `cline`, `codebuddy`, `codex`, `continue`, `costrict`, `crush`, `cursor`, `factory`, `gemini`, `github-copilot`, `iflow`, `kilocode`, `opencode`, `qoder`, `qwen`, `roocode`, `trae`, `windsurf`

## Что устанавливается

Для каждого инструмента OpenSpec генерирует 10 файлов навыков, которые обеспечивают работу процесса OPSX:

| Навык | Назначение |
|-------|---------|
| `openspec-explore` | Партнер для обсуждения и исследования идей |
| `openspec-new-change` | Начало нового изменения |
| `openspec-continue-change` | Создание следующего артефакта |
| `openspec-ff-change` | Быстрое создание всех артефактов планирования |
| `openspec-apply-change` | Выполнение задач |
| `openspec-verify-change` | Проверка полноты реализации |
| `openspec-sync-specs` | Синхронизация дельта-спецификаций с основными (опционально) |
| `openspec-archive-change` | Архивирование завершенного изменения |
| `openspec-bulk-archive-change` | Архивирование нескольких изменений одновременно |
| `openspec-onboard` | Пошаговое руководство через полный цикл рабочего процесса |

Эти навыки вызываются через слеш-команды, такие как `/opsx:new`, `/opsx:apply` и т. д. Полный список см. в разделе [Команды](commands.md).

## Добавление нового инструмента

Хотите добавить поддержку другого ИИ-ассистента? Ознакомьтесь с [паттерном адаптера команд](../CONTRIBUTING.md) или откройте issue на GitHub.

---

## Связанные разделы

- [Справочник CLI](cli.md) — команды терминала
- [Команды](commands.md) — слеш-команды и навыки
- [Начало работы](getting-started.md) — первая настройка
