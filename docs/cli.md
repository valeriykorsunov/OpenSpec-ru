# Справочник CLI (CLI Reference)

CLI OpenSpec (`openspec`) предоставляет терминальные команды для настройки проекта, валидации, проверки статуса и управления. Эти команды дополняют слеш-команды ИИ (такие как `/opsx:new`), описанные в разделе [Команды](commands.md).

## Сводка

| Категория | Команды | Назначение |
|----------|----------|---------|
| **Настройка** | `init`, `update` | Инициализация и обновление OpenSpec в вашем проекте |
| **Просмотр** | `list`, `view`, `show` | Просмотр изменений и спецификаций |
| **Валидация** | `validate` | Проверка изменений и спецификаций на наличие ошибок |
| **Жизненный цикл** | `archive` | Завершение выполненных изменений |
| **Рабочий процесс** | `status`, `instructions`, `templates`, `schemas` | Поддержка рабочего процесса на основе артефактов |
| **Схемы** | `schema init`, `schema fork`, `schema validate`, `schema which` | Создание и управление кастомными рабочими процессами |
| **Конфигурация** | `config` | Просмотр и изменение настроек |
| **Утилиты** | `feedback`, `completion` | Обратная связь и интеграция с оболочкой (shell) |

---

## Команды для человека и для агента

Большинство команд CLI предназначены для **использования человеком** в терминале. Некоторые команды также поддерживают **использование агентами/скриптами** через вывод в формате JSON.

### Команды только для человека

Эти команды являются интерактивными и предназначены для использования в терминале:

| Команда | Назначение |
|---------|---------|
| `openspec init` | Инициализация проекта (интерактивные подсказки) |
| `openspec view` | Интерактивный дашборд |
| `openspec config edit` | Открыть конфиг в редакторе |
| `openspec feedback` | Отправить отзыв через GitHub |
| `openspec completion install` | Установить автодополнение для оболочки |

### Команды, совместимые с агентами

Эти команды поддерживают опцию `--json` для программного использования ИИ-агентами и скриптами:

| Команда | Использование человеком | Использование агентом |
|---------|-----------|-----------|
| `openspec list` | Просмотр изменений/спецификаций | `--json` для структурированных данных |
| `openspec show <item>` | Чтение контента | `--json` для парсинга |
| `openspec validate` | Проверка на наличие проблем | `--all --json` для массовой валидации |
| `openspec status` | Просмотр прогресса артефактов | `--json` для структурированного статуса |
| `openspec instructions` | Получение следующих шагов | `--json` для инструкций агенту |
| `openspec templates` | Поиск путей к шаблонам | `--json` для разрешения путей |
| `openspec schemas` | Список доступных схем | `--json` для обнаружения схем |

---

## Глобальные опции

Эти опции работают со всеми командами:

| Опция | Описание |
|--------|-------------|
| `--version`, `-V` | Показать номер версии |
| `--no-color` | Отключить цветной вывод |
| `--help`, `-h` | Показать справку по команде |

---

## Команды настройки

### `openspec init`

Инициализация OpenSpec в вашем проекте. Создает структуру папок и настраивает интеграцию с ИИ-инструментами.

```
openspec init [path] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `path` | Нет | Целевая директория (по умолчанию: текущая директория) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--tools <list>` | Настроить ИИ-инструменты неинтерактивно. Используйте `all`, `none` или список через запятую |
| `--force` | Автоматическая очистка устаревших файлов без подтверждения |

**Поддерживаемые инструменты:** `amazon-q`, `antigravity`, `auggie`, `claude`, `cline`, `codex`, `codebuddy`, `continue`, `costrict`, `crush`, `cursor`, `factory`, `gemini`, `github-copilot`, `iflow`, `kilocode`, `opencode`, `qoder`, `qwen`, `roocode`, `windsurf`

**Примеры:**

```bash
# Интерактивная инициализация
openspec init

# Инициализация в конкретной директории
openspec init ./my-project

# Неинтерактивно: настройка для Claude и Cursor
openspec init --tools claude,cursor

# Настройка для всех поддерживаемых инструментов
openspec init --tools all

# Пропустить подсказки и автоматически очистить старые файлы
openspec init --force
```

**Что создается:**

```
openspec/
├── specs/              # Ваши спецификации (источник истины)
├── changes/            # Предлагаемые изменения
└── config.yaml         # Конфигурация проекта

.claude/skills/         # Файлы навыков Claude Code (если выбран claude)
.cursor/rules/          # Правила Cursor (если выбран cursor)
... (конфиги других инструментов)
```

---

### `openspec update`

Обновление файлов инструкций OpenSpec после обновления CLI. Перегенерирует файлы конфигурации ИИ-инструментов.

```
openspec update [path] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `path` | Нет | Целевая директория (по умолчанию: текущая директория) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--force` | Принудительное обновление, даже если файлы актуальны |

**Пример:**

```bash
# Обновление файлов инструкций после npm upgrade
npm update @fission-ai/openspec
openspec update
```

---

## Команды просмотра

### `openspec list`

Список изменений или спецификаций в вашем проекте.

```
openspec list [options]
```

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--specs` | Вывести список спецификаций вместо изменений |
| `--changes` | Вывести список изменений (по умолчанию) |
| `--sort <order>` | Сортировка по `recent` (недавние, по умолчанию) или `name` (по имени) |
| `--json` | Вывод в формате JSON |

**Примеры:**

```bash
# Список всех активных изменений
openspec list

# Список всех спецификаций
openspec list --specs

# Вывод в JSON для скриптов
openspec list --json
```

**Вывод (текст):**

```
Active changes:
  add-dark-mode     UI theme switching support
  fix-login-bug     Session timeout handling
```

---

### `openspec view`

Отображение интерактивного дашборда для изучения спецификаций и изменений.

```
openspec view
```

Открывает терминальный интерфейс для навигации по спецификациям и изменениям вашего проекта.

---

### `openspec show`

Отображение деталей изменения или спецификации.

```
openspec show [item-name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `item-name` | Нет | Имя изменения или спецификации (запрашивается, если опущено) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--type <type>` | Указать тип: `change` или `spec` (определяется автоматически, если нет двусмысленности) |
| `--json` | Вывод в формате JSON |
| `--no-interactive` | Отключить интерактивные подсказки |

**Опции только для изменений:**

| Опция | Описание |
|--------|-------------|
| `--deltas-only` | Показать только дельта-спецификации (в режиме JSON) |

**Опции только для спецификаций:**

| Опция | Описание |
|--------|-------------|
| `--requirements` | Показать только требования, исключить сценарии (в режиме JSON) |
| `--no-scenarios` | Исключить содержание сценариев (в режиме JSON) |
| `-r, --requirement <id>` | Показать конкретное требование по индексу (начиная с 1, в режиме JSON) |

**Примеры:**

```bash
# Интерактивный выбор
openspec show

# Показать конкретное изменение
openspec show add-dark-mode

# Показать конкретную спецификацию
openspec show auth --type spec

# Вывод в JSON для парсинга
openspec show add-dark-mode --json
```

---

## Команды валидации

### `openspec validate`

Валидация изменений и спецификаций на наличие структурных проблем.

```
openspec validate [item-name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `item-name` | Нет | Конкретный элемент для валидации (запрашивается, если опущено) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--all` | Валидация всех изменений и спецификаций |
| `--changes` | Валидация всех изменений |
| `--specs` | Валидация всех спецификаций |
| `--type <type>` | Указать тип, если имя двусмысленно: `change` или `spec` |
| `--strict` | Включить строгий режим валидации |
| `--json` | Вывод в формате JSON |
| `--concurrency <n>` | Максимальное количество параллельных валидаций (по умолчанию: 6 или переменная `OPENSPEC_CONCURRENCY`) |
| `--no-interactive` | Отключить интерактивные подсказки |

**Примеры:**

```bash
# Интерактивная валидация
openspec validate

# Валидация конкретного изменения
openspec validate add-dark-mode

# Валидация всех изменений
openspec validate --changes

# Валидация всего с выводом в JSON (для CI/скриптов)
openspec validate --all --json

# Строгая валидация с повышенным параллелизмом
openspec validate --all --strict --concurrency 12
```

**Вывод (текст):**

```
Validating add-dark-mode...
  ✓ proposal.md valid
  ✓ specs/ui/spec.md valid
  ⚠ design.md: missing "Technical Approach" section

1 warning found
```

**Вывод (JSON):**

```json
{
  "version": "1.0.0",
  "results": {
    "changes": [
      {
        "name": "add-dark-mode",
        "valid": true,
        "warnings": ["design.md: missing 'Technical Approach' section"]
      }
    ]
  },
  "summary": {
    "total": 1,
    "valid": 1,
    "invalid": 0
  }
}
```

---

## Команды жизненного цикла

### `openspec archive`

Архивация завершенного изменения и слияние дельта-спецификаций с основными спецификациями.

```
openspec archive [change-name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `change-name` | Нет | Изменение для архивации (запрашивается, если опущено) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `-y, --yes` | Пропустить подтверждение |
| `--skip-specs` | Пропустить обновление спецификаций (для изменений инфраструктуры/инструментария/только документации) |
| `--no-validate` | Пропустить валидацию (требует подтверждения) |

**Примеры:**

```bash
# Интерактивная архивация
openspec archive

# Архивация конкретного изменения
openspec archive add-dark-mode

# Архивация без подсказок (для CI/скриптов)
openspec archive add-dark-mode --yes

# Архивация изменения инструментов, которое не влияет на спецификации
openspec archive update-ci-config --skip-specs
```

**Что она делает:**

1. Валидирует изменение (если не указано `--no-validate`)
2. Запрашивает подтверждение (если не указано `--yes`)
3. Сливает дельта-спецификации в `openspec/specs/`
4. Перемещает папку изменения в `openspec/changes/archive/ГГГГ-ММ-ДД-<имя>/`

---

## Команды рабочего процесса

Эти команды поддерживают рабочий процесс OPSX на основе артефактов. Они полезны как для людей, проверяющих прогресс, так и для агентов, определяющих следующие шаги.

### `openspec status`

Отображение статуса завершения артефактов для изменения.

```
openspec status [options]
```

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--change <id>` | Имя изменения (запрашивается, если опущено) |
| `--schema <name>` | Переопределение схемы (автоматически определяется из конфига изменения) |
| `--json` | Вывод в формате JSON |

**Примеры:**

```bash
# Интерактивная проверка статуса
openspec status

# Статус для конкретного изменения
openspec status --change add-dark-mode

# JSON для использования агентом
openspec status --change add-dark-mode --json
```

**Вывод (текст):**

```
Change: add-dark-mode
Schema: spec-driven

Artifacts:
  ✓ proposal     proposal.md exists
  ✓ specs        specs/ exists
  ◆ design       ready (requires: specs)
  ○ tasks        blocked (requires: design)

Next: Create design using /opsx:continue
```

**Вывод (JSON):**

```json
{
  "change": "add-dark-mode",
  "schema": "spec-driven",
  "artifacts": [
    {"id": "proposal", "status": "complete", "path": "proposal.md"},
    {"id": "specs", "status": "complete", "path": "specs/"},
    {"id": "design", "status": "ready", "requires": ["specs"]},
    {"id": "tasks", "status": "blocked", "requires": ["design"]}
  ],
  "next": "design"
}
```

---

### `openspec instructions`

Получение расширенных инструкций для создания артефакта или реализации задач. Используется ИИ-агентами для понимания того, что создавать дальше.

```
openspec instructions [artifact] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `artifact` | Нет | ID артефакта: `proposal`, `specs`, `design`, `tasks` или `apply` |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--change <id>` | Имя изменения (обязательно в неинтерактивном режиме) |
| `--schema <name>` | Переопределение схемы |
| `--json` | Вывод в формате JSON |

**Особый случай:** Используйте `apply` в качестве артефакта, чтобы получить инструкции по реализации задач.

**Примеры:**

```bash
# Получить инструкции для следующего артефакта
openspec instructions --change add-dark-mode

# Получить инструкции для конкретного артефакта
openspec instructions design --change add-dark-mode

# Получить инструкции по реализации (apply)
openspec instructions apply --change add-dark-mode

# JSON для использования агентом
openspec instructions design --change add-dark-mode --json
```

**Вывод включает:**

- Содержимое шаблона для артефакта
- Контекст проекта из конфига
- Содержимое зависимых артефактов
- Правила для конкретного артефакта из конфига

---

### `openspec templates`

Показать разрешенные пути к шаблонам для всех артефактов в схеме.

```
openspec templates [options]
```

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--schema <name>` | Схема для проверки (по умолчанию: `spec-driven`) |
| `--json` | Вывод в формате JSON |

**Примеры:**

```bash
# Показать пути к шаблонам для схемы по умолчанию
openspec templates

# Показать шаблоны для кастомной схемы
openspec templates --schema my-workflow

# JSON для программного использования
openspec templates --json
```

**Вывод (текст):**

```
Schema: spec-driven

Templates:
  proposal  → ~/.openspec/schemas/spec-driven/templates/proposal.md
  specs     → ~/.openspec/schemas/spec-driven/templates/specs.md
  design    → ~/.openspec/schemas/spec-driven/templates/design.md
  tasks     → ~/.openspec/schemas/spec-driven/templates/tasks.md
```

---

### `openspec schemas`

Список доступных схем рабочих процессов с их описаниями и потоками артефактов.

```
openspec schemas [options]
```

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--json` | Вывод в формате JSON |

**Пример:**

```bash
openspec schemas
```

**Вывод:**

```
Available schemas:

  spec-driven (package)
    The default spec-driven development workflow
    Flow: proposal → specs → design → tasks

  my-custom (project)
    Custom workflow for this project
    Flow: research → proposal → tasks
```

---

## Команды схем (Schema Commands)

Команды для создания и управления кастомными схемами рабочих процессов.

### `openspec schema init`

Создание новой локальной схемы проекта.

```
openspec schema init <name> [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `name` | Да | Имя схемы (в формате kebab-case) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--description <text>` | Описание схемы |
| `--artifacts <list>` | Список ID артефактов через запятую (по умолчанию: `proposal,specs,design,tasks`) |
| `--default` | Установить как схему по умолчанию для проекта |
| `--no-default` | Не предлагать установку в качестве схемы по умолчанию |
| `--force` | Перезаписать существующую схему |
| `--json` | Вывод в формате JSON |

**Примеры:**

```bash
# Интерактивное создание схемы
openspec schema init research-first

# Неинтерактивно с конкретными артефактами
openspec schema init rapid \
  --description "Rapid iteration workflow" \
  --artifacts "proposal,tasks" \
  --default
```

**Что создается:**

```
openspec/schemas/<name>/
├── schema.yaml           # Определение схемы
└── templates/
    ├── proposal.md       # Шаблон для каждого артефакта
    ├── specs.md
    ├── design.md
    └── tasks.md
```

---

### `openspec schema fork`

Копирование существующей схемы в проект для кастомизации.

```
openspec schema fork <source> [name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `source` | Да | Схема для копирования |
| `name` | Нет | Имя новой схемы (по умолчанию: `<source>-custom`) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--force` | Перезаписать существующую целевую схему |
| `--json` | Вывод в формате JSON |

**Пример:**

```bash
# Форк встроенной схемы spec-driven
openspec schema fork spec-driven my-workflow
```

---

### `openspec schema validate`

Валидация структуры схемы и её шаблонов.

```
openspec schema validate [name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `name` | Нет | Схема для валидации (валидирует все, если опущено) |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--verbose` | Показать подробные шаги валидации |
| `--json` | Вывод в формате JSON |

**Пример:**

```bash
# Валидация конкретной схемы
openspec schema validate my-workflow

# Валидация всех схем
openspec schema validate
```

---

### `openspec schema which`

Показать, откуда разрешается схема (полезно для отладки приоритетов).

```
openspec schema which [name] [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `name` | Нет | Имя схемы |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--all` | Список всех схем с их источниками |
| `--json` | Вывод в формате JSON |

**Пример:**

```bash
# Проверить источник схемы
openspec schema which spec-driven
```

**Вывод:**

```
spec-driven resolves from: package
  Source: /usr/local/lib/node_modules/@fission-ai/openspec/schemas/spec-driven
```

**Приоритет схем:**

1. Проект: `openspec/schemas/<name>/`
2. Пользователь: `~/.local/share/openspec/schemas/<name>/`
3. Пакет: Встроенные схемы

---

## Команды конфигурации

### `openspec config`

Просмотр и изменение глобальной конфигурации OpenSpec.

```
openspec config <subcommand> [options]
```

**Подкоманды:**

| Подкоманда | Описание |
|------------|-------------|
| `path` | Показать путь к файлу конфигурации |
| `list` | Показать все текущие настройки |
| `get <key>` | Получить конкретное значение |
| `set <key> <value>` | Установить значение |
| `unset <key>` | Удалить ключ |
| `reset` | Сбросить до настроек по умолчанию |
| `edit` | Открыть в `$EDITOR` |

**Примеры:**

```bash
# Показать путь к файлу конфига
openspec config path

# Список всех настроек
openspec config list

# Получить конкретное значение
openspec config get telemetry.enabled

# Установить значение
openspec config set telemetry.enabled false

# Явно установить строковое значение
openspec config set user.name "My Name" --string

# Удалить пользовательскую настройку
openspec config unset user.name

# Сбросить всю конфигурацию
openspec config reset --all --yes

# Редактировать конфиг в вашем редакторе
openspec config edit
```

---

## Утилиты

### `openspec feedback`

Отправить отзыв об OpenSpec. Создает issue на GitHub.

```
openspec feedback <message> [options]
```

**Аргументы:**

| Аргумент | Обязательный | Описание |
|----------|----------|-------------|
| `message` | Да | Сообщение отзыва |

**Опции:**

| Опция | Описание |
|--------|-------------|
| `--body <text>` | Подробное описание |

**Требования:** Должен быть установлен и аутентифицирован GitHub CLI (`gh`).

**Пример:**

```bash
openspec feedback "Add support for custom artifact types" \
  --body "I'd like to define my own artifact types beyond the built-in ones."
```

---

### `openspec completion`

Управление автодополнением команд OpenSpec в оболочке.

```
openspec completion <subcommand> [shell]
```

**Подкоманды:**

| Подкоманда | Описание |
|------------|-------------|
| `generate [shell]` | Вывести скрипт автодополнения в stdout |
| `install [shell]` | Установить автодополнение для вашей оболочки |
| `uninstall [shell]` | Удалить установленные автодополнения |

**Поддерживаемые оболочки:** `bash`, `zsh`, `fish`, `powershell`

**Примеры:**

```bash
# Установить автодополнение (автоопределение оболочки)
openspec completion install

# Установить для конкретной оболочки
openspec completion install zsh

# Генерация скрипта для ручной установки
openspec completion generate bash > ~/.bash_completion.d/openspec

# Удалить
openspec completion uninstall
```

---

## Коды выхода (Exit Codes)

| Код | Значение |
|------|---------|
| `0` | Успех |
| `1` | Ошибка (ошибка валидации, отсутствие файлов и т.д.) |

---

## Переменные окружения

| Переменная | Описание |
|----------|-------------|
| `OPENSPEC_CONCURRENCY` | Параллелизм по умолчанию для массовой валидации (по умолчанию: 6) |
| `EDITOR` или `VISUAL` | Редактор для `openspec config edit` |
| `NO_COLOR` | Отключить цветной вывод при установке |

---

## Связанная документация

- [Команды](commands.md) — слеш-команды ИИ (`/opsx:new`, `/opsx:apply` и т.д.)
- [Процессы](workflows.md) — распространенные паттерны и информация о том, когда использовать каждую команду
- [Кастомизация](customization.md) — создание кастомных схем и шаблонов
- [Начало работы](getting-started.md) — руководство по первой настройке
