<p align="center">
  <a href="https://github.com/Fission-AI/OpenSpec">
    <picture>
      <source srcset="assets/openspec_bg.png">
      <img src="assets/openspec_bg.png" alt="OpenSpec logo">
    </picture>
  </a>
</p>

<p align="center">
  <a href="https://github.com/Fission-AI/OpenSpec/actions/workflows/ci.yml"><img alt="CI" src="https://github.com/Fission-AI/OpenSpec/actions/workflows/ci.yml/badge.svg" /></a>
  <a href="https://www.npmjs.com/package/@fission-ai/openspec"><img alt="npm version" src="https://img.shields.io/npm/v/@fission-ai/openspec?style=flat-square" /></a>
  <a href="./LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square" /></a>
  <a href="https://discord.gg/YctCnvvshC"><img alt="Discord" src="https://img.shields.io/discord/1411657095639601154?style=flat-square&logo=discord&logoColor=white&label=Discord&suffix=%20online" /></a>
</p>

<details>
<summary><strong>Самый любимый фреймворк спецификаций.</strong></summary>

[![Stars](https://img.shields.io/github/stars/Fission-AI/OpenSpec?style=flat-square&label=Stars)](https://github.com/Fission-AI/OpenSpec/stargazers)
[![Downloads](https://img.shields.io/npm/dm/@fission-ai/openspec?style=flat-square&label=Downloads/mo)](https://www.npmjs.com/package/@fission-ai/openspec)
[![Contributors](https://img.shields.io/github/contributors/Fission-AI/OpenSpec?style=flat-square&label=Contributors)](https://github.com/Fission-AI/OpenSpec/graphs/contributors)

</details>
<p></p>
Наша философия:

```text
→ гибкость, а не жесткость
→ итеративность, а не водопад (waterfall)
→ простота, а не сложность
→ создано для существующих проектов (brownfield), а не только для новых (greenfield)
→ масштабируемость от личных проектов до корпоративных
```

> [!TIP]
> **Доступен новый рабочий процесс!** Мы перестроили OpenSpec с новым рабочим процессом, ориентированным на артефакты.
>
> Запустите `/opsx:onboard`, чтобы начать. → [Узнайте больше здесь](docs/opsx.md)

<p align="center">
  Следите за <a href="https://x.com/0xTab">@0xTab в X</a> для обновлений · Присоединяйтесь к <a href="https://discord.gg/YctCnvvshC">OpenSpec Discord</a> для помощи и вопросов.
</p>

### Команды

Используете OpenSpec в команде? [Напишите сюда](mailto:teams@openspec.dev) для доступа к нашему каналу в Slack.

<!-- TODO: Добавить GIF-демонстрацию рабочего процесса /opsx:new → /opsx:archive -->

## Посмотрите в действии

```text
Вы: /opsx:new add-dark-mode
ИИ: Создан openspec/changes/add-dark-mode/
     Готов создать: proposal (предложение)

Вы: /opsx:ff   # "fast-forward" - сгенерировать все документы планирования
ИИ:  ✓ proposal.md — зачем мы это делаем, что меняется
     ✓ specs/       — требования и сценарии
     ✓ design.md    — технический подход
     ✓ tasks.md     — чек-лист реализации
     Готово к реализации!

Вы: /opsx:apply
ИИ:  Реализация задач...
     ✓ 1.1 Добавить провайдер контекста темы
     ✓ 1.2 Создать компонент переключателя
     ✓ 2.1 Добавить CSS переменные
     ✓ 2.2 Подключить localStorage
     Все задачи выполнены!

Вы: /opsx:archive
ИИ:  Заархивировано в openspec/changes/archive/2025-01-23-add-dark-mode/
     Спецификации обновлены. Готов к следующей функции.
```

<details>
<summary><strong>Панель управления OpenSpec</strong></summary>

<p align="center">
  <img src="assets/openspec_dashboard.png" alt="Предварительный просмотр панели OpenSpec" width="90%">
</p>

</details>

## Быстрый старт

**Требуется Node.js 20.19.0 или выше.**

Установите OpenSpec глобально:

```bash
npm install -g @fission-ai/openspec@latest
```

Затем перейдите в директорию вашего проекта и инициализируйте:

```bash
cd your-project
openspec init
```

Теперь скажите вашему ИИ: `/opsx:new <что-вы-хотите-создать>`

> [!NOTE]
> Не уверены, поддерживается ли ваш инструмент? [Посмотрите полный список](docs/supported-tools.md) – мы поддерживаем 20+ инструментов, и список растет.
>
> Также работает с pnpm, yarn, bun и nix. [См. варианты установки](docs/installation.md).

## Документация

→ **[Начало работы](docs/getting-started.md)**: первые шаги<br>
→ **[Рабочие процессы](docs/workflows.md)**: комбинации и паттерны<br>
→ **[Команды](docs/commands.md)**: слэш-команды и навыки<br>
→ **[CLI](docs/cli.md)**: справочник терминала<br>
→ **[Поддерживаемые инструменты](docs/supported-tools.md)**: интеграции инструментов и пути установки<br>
→ **[Концепции](docs/concepts.md)**: как это всё работает вместе<br>
→ **[Мультиязычность](docs/multi-language.md)**: поддержка нескольких языков<br>
→ **[Кастомизация](docs/customization.md)**: сделайте его своим

## Почему OpenSpec?

ИИ-ассистенты для кодинга мощны, но непредсказуемы, когда требования живут только в истории чата. OpenSpec добавляет легкий слой спецификаций, чтобы вы согласовали, что строить, до того, как будет написан код.

- **Согласуйте перед созданием** — человек и ИИ согласовывают спецификации до написания кода
- **Оставайтесь организованными** — каждое изменение получает свою папку с предложением, спецификациями, дизайном и задачами
- **Работайте гибко** — обновляйте любой артефакт в любое время, без жестких этапов
- **Используйте свои инструменты** — работает с 20+ ИИ-ассистентами через слэш-команды

### Сравнение

**vs. [Spec Kit](https://github.com/github/spec-kit)** (GitHub) — Тщательный, но тяжеловесный. Жесткие этапы, много Markdown, установка Python. OpenSpec легче и позволяет итерироваться свободно.

**vs. [Kiro](https://kiro.dev)** (AWS) — Мощный, но вы заперты в их IDE и ограничены моделями Claude. OpenSpec работает с инструментами, которые вы уже используете.

**vs. ничего** — ИИ-кодинг без спецификаций означает расплывчатые промпты и непредсказуемые результаты. OpenSpec привносит предсказуемость без лишних церемоний.

## Обновление OpenSpec

**Обновить пакет**

```bash
npm install -g @fission-ai/openspec@latest
```

**Обновить инструкции агента**

Запустите это внутри каждого проекта, чтобы перегенерировать руководство для ИИ и убедиться, что активны последние слэш-команды:

```bash
openspec update
```

## Примечания по использованию

**Выбор модели**: OpenSpec лучше всего работает с моделями с высоким уровнем рассуждений. Мы рекомендуем Opus 4.5 и GPT 5.2 как для планирования, так и для реализации.

**Гигиена контекста**: OpenSpec выигрывает от чистого окна контекста. Очищайте контекст перед началом реализации и поддерживайте хорошую гигиену контекста на протяжении всей сессии.

## Участие в разработке (Contributing)

**Небольшие исправления** — Исправления ошибок, опечаток и незначительные улучшения можно отправлять напрямую в виде PR.

**Более крупные изменения** — Для новых функций, значительного рефакторинга или архитектурных изменений, пожалуйста, сначала отправьте предложение по изменению OpenSpec, чтобы мы могли согласовать намерения и цели до начала реализации.

При написании предложений помните о философии OpenSpec: мы обслуживаем широкий круг пользователей с разными агентами кодинга, моделями и вариантами использования. Изменения должны хорошо работать для всех.

**ИИ-генерированный код приветствуется** — при условии, что он был протестирован и проверен. PR, содержащие код, сгенерированный ИИ, должны упоминать использованного агента и модель (например, "Сгенерировано с помощью Claude Code используя claude-opus-4-5-20251101").

### Разработка

- Установка зависимостей: `pnpm install`
- Сборка: `pnpm run build`
- Тест: `pnpm test`
- Локальная разработка CLI: `pnpm run dev` или `pnpm run dev:cli`
- Обычные коммиты (в одну строку): `type(scope): subject`

## Другое

<details>
<summary><strong>Телеметрия</strong></summary>

OpenSpec собирает анонимную статистику использования.

Мы собираем только имена команд и версию, чтобы понимать паттерны использования. Никаких аргументов, путей, контента или PII (персональных данных). Автоматически отключено в CI.

**Отказаться:** `export OPENSPEC_TELEMETRY=0` или `export DO_NOT_TRACK=1`

</details>

<details>
<summary><strong>Мейнтейнеры и Советники</strong></summary>

Смотрите [MAINTAINERS.md](MAINTAINERS.md) для списка основных мейнтейнеров и советников, которые помогают направлять проект.

</details>



## Лицензия

MIT
