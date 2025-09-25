# OpenCCK Clash Rules

[English Version](README.md) | Русская версия

Этот проект генерирует правила для [Clash Premium](https://github.com/Dreamacro/clash/releases/tag/premium) на основе списков доменов от [OpenCCK](https://iplist.opencck.org/). Автоматическая сборка происходит ежедневно в 21:00 UTC с использованием GitHub Actions.

## Доступные списки правил

### Онлайн адреса (URL)

Используйте эти URL в конфигурации Clash в секции `rule-providers`:

- **Порнографические сайты (porno.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/porno.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/porno.txt`

- **Discord (discord.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/discord.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/discord.txt`

- **YouTube (youtube.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/youtube.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/youtube.txt`

- **Социальные сети (socials.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/socials.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/socials.txt`

- **Торренты (torrent.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/torrent.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/torrent.txt`

- **Инструменты разработки (tools.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/tools.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/tools.txt`

- **Музыкальные сервисы (music.txt)**:
  - `https://raw.githubusercontent.com/nellimonix/ClashXRule/release/music.txt`
  - `https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/music.txt`

## Использование

### Конфигурация Rule Providers

```yaml
rule-providers:
  porno:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/porno.txt"
    path: ./ruleset/porno.yaml
    interval: 86400

  discord:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/discord.txt"
    path: ./ruleset/discord.yaml
    interval: 86400

  youtube:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/youtube.txt"
    path: ./ruleset/youtube.yaml
    interval: 86400

  socials:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/socials.txt"
    path: ./ruleset/socials.yaml
    interval: 86400

  torrent:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/torrent.txt"
    path: ./ruleset/torrent.yaml
    interval: 86400

  tools:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/tools.txt"
    path: ./ruleset/tools.yaml
    interval: 86400

  music:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/nellimonix/ClashXRule@release/music.txt"
    path: ./ruleset/music.yaml
    interval: 86400
```

### Примеры конфигурации правил

#### Режим фильтрации контента

```yaml
rules:
  # Заблокировать порнографические сайты
  - RULE-SET,porno,REJECT
  
  # Перенаправить через прокси социальные сети и мессенджеры
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  
  # Заблокировать торренты
  - RULE-SET,torrent,REJECT
  
  # Разрешить инструменты разработки напрямую
  - RULE-SET,tools,DIRECT
  
  # Перенаправить музыкальные сервисы через прокси
  - RULE-SET,music,PROXY
  
  # Остальной трафик
  - MATCH,DIRECT
```

#### Режим обхода цензуры

Если вы находитесь в регионе с интернет-ограничениями и хотите их обходить:

```yaml
rules:
  # Обходить ограничения через прокси
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  - RULE-SET,music,PROXY
  - RULE-SET,tools,PROXY
  
  # Опционально: блокировать торренты для экономии трафика
  - RULE-SET,torrent,REJECT
  
  # Опционально: блокировать порнографию
  - RULE-SET,porno,REJECT
  
  # Остальной трафик напрямую
  - MATCH,DIRECT
```

#### Режим родительского контроля

```yaml
rules:
  # Заблокировать неподходящий контент
  - RULE-SET,porno,REJECT
  - RULE-SET,torrent,REJECT
  
  # Разрешить образовательные и рабочие инструменты
  - RULE-SET,tools,DIRECT
  
  # Контролировать доступ к соцсетям (можно установить REJECT при необходимости)
  - RULE-SET,discord,PROXY
  - RULE-SET,socials,PROXY
  - RULE-SET,youtube,PROXY
  - RULE-SET,music,PROXY
  
  # Остальной трафик
  - MATCH,DIRECT
```

## Источники данных

Все правила генерируются на основе списков доменов от [OpenCCK](https://iplist.opencck.org/):

- Порнография: https://iplist.opencck.org/?format=text&data=domains&group=porn
- Discord: https://iplist.opencck.org/?format=text&data=domains&group=discord
- YouTube: https://iplist.opencck.org/?format=text&data=domains&group=youtube
- Социальные сети: https://iplist.opencck.org/?format=text&data=domains&group=socials
- Торренты: https://iplist.opencck.org/?format=text&data=domains&group=torrent
- Инструменты разработки: https://iplist.opencck.org/?format=text&data=domains&group=tools
- Музыкальные сервисы: https://iplist.opencck.org/?format=text&data=domains&group=music

## Установка

1. Создайте новый репозиторий на GitHub
2. Скопируйте файлы из этого проекта
3. Замените `nellimonix/ClashXRule` в README на реальные значения
4. Включите GitHub Actions в настройках репозитория
5. Запустите workflow вручную или дождитесь автоматического выполнения

## Особенности

- **Ежедневные обновления**: Автоматическая генерация правил каждый день в 06:00 UTC
- **Множество категорий**: 7 различных категорий правил для гибкого управления трафиком
- **Поддержка CDN**: Файлы доступны через GitHub raw URL и jsDelivr CDN
- **Поддержка wildcards**: Правильная обработка доменных wildcards для полного покрытия
- **Совместимость с Clash Premium**: Оптимизировано для ядра Clash Premium

## Лицензия

Этот проект лицензирован под GNU General Public License v3.0 - см. файл [LICENSE](LICENSE) для подробностей.

## Благодарности

- [OpenCCK](https://iplist.opencck.org/) за предоставление комплексных списков доменов
- [Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules) за вдохновение и структуру проекта
- Сообществу открытого исходного кода за постоянные улучшения