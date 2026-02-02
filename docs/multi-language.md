# Руководство по мультиязычности

Настройте OpenSpec для генерации артефактов на языках, отличных от английского.

## Быстрая настройка

Добавьте языковую инструкцию в ваш `openspec/config.yaml`:

```yaml
schema: spec-driven

context: |
  Language: Portuguese (pt-BR)
  All artifacts must be written in Brazilian Portuguese.

  # Другой контекст вашего проекта ниже...
  Tech stack: TypeScript, React, Node.js
```

Вот и всё. Все сгенерированные артефакты теперь будут на португальском языке.

## Примеры языков

### Португальский (Бразилия)

```yaml
context: |
  Language: Portuguese (pt-BR)
  All artifacts must be written in Brazilian Portuguese.
```

### Испанский

```yaml
context: |
  Idioma: Español
  Todos los artefactos deben escribirse en español.
```

### Китайский (Упрощенный)

```yaml
context: |
  语言：中文（简体）
  所有产出物必须用简体中文撰写。
```

### Японский

```yaml
context: |
  言語：日本語
  すべての成果物は日本語で作成してください。
```

### Французский

```yaml
context: |
  Langue : Français
  Tous les artefacts doivent être rédigés en français.
```

### Немецкий

```yaml
context: |
  Sprache: Deutsch
  Alle Artefakte müssen auf Deutsch verfasst werden.
```

### Русский

```yaml
context: |
  Language: Russian
  All artifacts must be written in Russian.
```

## Советы

### Обработка технических терминов

Решите, как обрабатывать техническую терминологию:

```yaml
context: |
  Language: Japanese
  Write in Japanese, but:
  - Keep technical terms like "API", "REST", "GraphQL" in English
  - Code examples and file paths remain in English
```

### Сочетание с другим контекстом

Настройки языка работают вместе с другим контекстом вашего проекта:

```yaml
schema: spec-driven

context: |
  Language: Portuguese (pt-BR)
  All artifacts must be written in Brazilian Portuguese.

  Tech stack: TypeScript, React 18, Node.js 20
  Database: PostgreSQL with Prisma ORM
```

## Проверка

Чтобы проверить, что конфигурация языка работает:

```bash
# Проверьте инструкции - должен отображаться ваш языковой контекст
openspec instructions proposal --change my-change

# Вывод будет включать ваш языковой контекст
```

## Связанная документация

- [Руководство по настройке](./customization.md) - Опции конфигурации проекта
- [Руководство по рабочим процессам](./workflows.md) - Полная документация рабочих процессов
