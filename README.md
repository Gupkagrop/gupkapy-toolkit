<div align="center">

# 🧰 GupkaPy Toolkit

**Модульная, строго типизированная библиотека легковесных структур данных, алгоритмов и прикладных утилит на чистом Python ($\ge 3.12$) без внешних зависимостей времени выполнения.**

[![CI](https://github.com/Gupkagrop/gupkapy-toolkit/actions/workflows/ci.yml/badge.svg)](https://github.com/Gupkagrop/gupkapy-toolkit/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/Gupkagrop/gupkapy-toolkit?color=007ec6&logo=github)](https://github.com/Gupkagrop/gupkapy-toolkit/releases)
[![Roadmap](https://img.shields.io/badge/Roadmap-60%2F60%20Completed-brightgreen.svg?style=flat)](ROADMAP.md)
[![Python 3.12 | 3.13](https://img.shields.io/badge/Python-3.12%20%7C%203.13-3776AB.svg?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![Tests](https://img.shields.io/badge/Tests-623%20passed-success.svg?style=flat&logo=pytest&logoColor=white)](https://github.com/Gupkagrop/gupkapy-toolkit/actions)
[![Dependencies](https://img.shields.io/badge/Dependencies-0%20(Pure%20Python)-blueviolet.svg?style=flat)](pyproject.toml)
[![Typing](https://img.shields.io/badge/Typing-Strict%20(0%20Any)-2ba244.svg?style=flat)](src/pocket_toolkit)
[![Code style](https://img.shields.io/badge/Code%20Style-Ruff-black.svg?style=flat&logo=ruff&logoColor=white)](https://github.com/astral-sh/ruff)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](LICENSE)

[Возможности](#-ключевые-особенности) • [Архитектура](#-архитектура-пакета) • [Примеры](#-примеры-использования) • [Разработка](#-разработка-и-тестирование) • [Дорожная карта](#-дорожная-карта)

</div>

---

## ✨ Ключевые особенности

* **Zero Dependencies** — работает исключительно на базе стандартной библиотеки Python 3.12+. Никаких транзитивных уязвимостей и накладных расходов.
* **Строгая типизация (Strict Typing)** — нулевая терпимость к `Any`. Каждый класс, метод и функция аннотированы дженериками (`TypeVar`, `Generic`) для мгновенного автодополнения в IDE.
* **Высокая производительность** — структуры данных с $O(1)$ и $O(\log n)$ характеристиками, сжатие RLE/Huffman, поиск KMP и Dijkstra.
* **Паттерны отказоустойчивости** — встроенные декораторы `@retry` с экспоненциальной задержкой и джиттером, алгоритмы `RateLimiter` (Token Bucket, Leaky Bucket) и `CircuitBreaker`.
* **Всестороннее тестирование** — 623 изолированных модульных теста, проходящих в CI менее чем за 1.5 секунды.
* **Плоский и чистый код** — соблюдение принципа Early Return (вложенность $\le 3$ уровней) и разделение ответственности.

---

## 🏛️ Архитектура пакета

Библиотека разделена на 8 изолированных субпакетов. Все публичные символы доступны как напрямую из `pocket_toolkit`, так и через специализированные модули:

```
src/pocket_toolkit/
├── structures/     # 12 структур данных (RingBuffer, LRU/LFU, Trie, RadixTree, Heap, BloomFilter...)
├── algorithms/     # 12 алгоритмов (поиск, Левенштейн, RLE, KMP, Хаффман, Дейкстра, топосорт...)
├── decorators/     # 6 декораторов отказоустойчивости (Retry, RateLimiter, LeakyBucket, CircuitBreaker...)
├── functional/     # 6 утилит функционального программирования (Pipe, Compose, Curry, LazyProperty...)
├── strings/        # 8 строковых утилит (Slugify, Case, Byte/Duration formatters, SemVer 2.0, Template...)
├── data/           # 6 утилит обработки данных (Flatten/Unflatten, DeepMerge/Patch, DictDiff, MathAST...)
├── cli/            # 4 консольные утилиты (ANSI Colors, Unicode Table, Progress Bar, Argument Parser)
└── system/         # 8 системных утилит (Env Parser, Glob, Temp, MemoryBuffer, AtomicWriter, Logger...)
```

### Сводная таблица компонентов

| Субпакет | Компонентов | Ключевые сущности | Назначение |
|:---|:---:|:---|:---|
| [`structures`](src/pocket_toolkit/structures) | 12 | `RingBuffer`, `LRUCache`, `LFUCache`, `Trie`, `RadixTree`, `PriorityQueue`, `DisjointSet`, `BloomFilter`, `BoundedDeque`, `SparseMatrix`, `LinkedList`, `DoublyLinkedList` | Высокоэффективные структуры хранения и организации данных |
| [`algorithms`](src/pocket_toolkit/algorithms) | 12 | `binary_search`, `levenshtein_distance`, `rle_encode`, `topological_sort`, `merge_intervals`, `kmp_search`, `huffman_encode`, `dijkstra`, `fast_power`, `crc32`, `reservoir_sample` | Классические и оптимизированные алгоритмы вычислений |
| [`decorators`](src/pocket_toolkit/decorators) | 6 | `@retry`, `@rate_limit`, `@leaky_bucket`, `@timed_cache`, `CircuitBreaker`, `@debounce`, `@throttle` | Отказоустойчивость, лимитирование трафика и управление вызовами |
| [`functional`](src/pocket_toolkit/functional) | 6 | `pipe`, `compose`, `@lazy_property`, `curry`, `@profile_time`, `@deprecated`, `@validate_types` | Функциональные пайплайны, профилирование и валидация контрактов |
| [`strings`](src/pocket_toolkit/strings) | 8 | `slugify`, `to_camel_case`, `to_snake_case`, `format_bytes`, `format_duration`, `SemanticVersion`, `render_template`, `build_query_string` | Трансформация строк, парсинг SemVer 2.0 и шаблонизация |
| [`data`](src/pocket_toolkit/data) | 6 | `flatten_dict`, `unflatten_dict`, `deep_merge`, `diff_dict`, `evaluate_math`, `parse_csv_stream` | Нормализация структур, слияние JSON/Dict и безопасный расчет формул |
| [`cli`](src/pocket_toolkit/cli) | 4 | `colorize`, `Table`, `ProgressBar`, `ArgumentParser` | Цветной вывод в терминал, форматирование таблиц и индикация прогресса |
| [`system`](src/pocket_toolkit/system) | 8 | `load_env`, `match_glob`, `temp_directory`, `MemoryBuffer`, `atomic_write`, `SimpleLogger`, `EventBus`, `collect_system_diagnostics` | Ввод-вывод, работа с файловой системой, переменные окружения и события |

---

## 🚀 Примеры использования

### 1. Структуры данных и кэширование
```python
from pocket_toolkit import LRUCache, PriorityQueue, RingBuffer

# Кольцевой буфер фиксированного размера
ring = RingBuffer[int](capacity=3)
ring.extend([1, 2, 3, 4])
print(list(ring))  # [2, 3, 4]

# LRU кэш с константным временем доступа O(1)
cache = LRUCache[str, str](capacity=2)
cache.put("a", "alpha")
cache.put("b", "beta")
cache.get("a")           # Обновляет свежесть записи
cache.put("c", "gamma")  # Автоматически вытесняет ключ "b"
```

### 2. Паттерны отказоустойчивости
```python
from pocket_toolkit import CircuitBreaker, rate_limit, retry

# Повторы при сбоях с экспоненциальной задержкой и джиттером
@retry(max_attempts=3, base_delay=0.5, backoff_factor=2.0)
def fetch_api() -> dict[str, str]:
    return {"status": "ok"}

# Ограничение частоты вызовов (Token Bucket)
@rate_limit(rate=10, capacity=10)
def handle_request(user_id: int) -> None:
    pass

# Защитный выключатель при каскадных сбоях
breaker = CircuitBreaker(failure_threshold=5, recovery_timeout=30.0)

@breaker
def query_microservice() -> str:
    return "response"
```

### 3. Функциональные пайплайны
```python
from pocket_toolkit import compose, pipe

# Линейный пайплайн преобразования данных
result = pipe(
    "  hello, world!  ",
    str.strip,
    str.upper,
    lambda s: s.replace("WORLD", "PYTHON")
)
print(result)  # "HELLO, PYTHON!"

# Композиция функций: (f ∘ g)(x)
double_and_increment = compose(lambda x: x + 1, lambda x: x * 2)
print(double_and_increment(5))  # 11
```

### 4. Строки, SemVer и безопасные вычисления
```python
from pocket_toolkit import (
    SemanticVersion,
    evaluate_math,
    format_bytes,
    format_duration,
    render_template,
)

# Человекочитаемое форматирование
print(format_bytes(1048576 * 2.5))  # "2.50 MiB"
print(format_duration(3665))        # "1ч 1м 5с"

# Безопасный калькулятор выражений на базе AST (без вызова eval)
calc_result = evaluate_math("2 * (x + 5) ^ 2", variables={"x": 5})  # 200.0

# Семантическое версионирование (SemVer 2.0)
v1 = SemanticVersion.parse("1.2.3-alpha.1")
v2 = v1.bump_minor()
print(v2)       # "1.3.0"
print(v1 < v2)  # True

# Легковесный шаблонизатор текста
template = "Здравствуйте, {{ user.name }}! {% if is_admin %}Доступ разрешен.{% endif %}"
output = render_template(template, {"user": {"name": "Денис"}, "is_admin": True})
```

### 5. Консольные интерфейсы и системные утилиты
```python
from pocket_toolkit import (
    EventBus,
    ProgressBar,
    Table,
    atomic_write,
    green,
    load_env,
)

# Вывод аккуратных Unicode-таблиц
table = Table(headers=["Модуль", "Статус"], style="unicode")
table.add_row("API Gateway", green("ONLINE"))
table.add_row("Cache Engine", green("ONLINE"))
print(table.render())

# Атомарная запись без риска повреждения файла
atomic_write("config.json", '{"mode": "production"}')

# Потокобезопасная синхронная шина событий
bus = EventBus()

@bus.on("user.login")
def on_login(event: object) -> None:
    print(f"Событие авторизации: {event}")

bus.publish("user.login", {"user_id": 42})
```

---

## 🛠️ Разработка и тестирование

### Требования
* Python $\ge 3.12$
* [uv](https://docs.astral.sh/uv/) — современный быстрый менеджер проектов Python

### Клонирование и настройка окружения
```bash
# Клонирование репозитория
git clone https://github.com/Gupkagrop/gupkapy-toolkit.git
cd gupkapy-toolkit

# Синхронизация зависимостей окружения разработки
uv sync
```

### Запуск тестов и линтера
```bash
# Запуск модульных тестов (623 теста)
uv run pytest

# Проверка стиля кода и статический анализ
uv run ruff check .

# Сборка дистрибутива (Wheel и sdist)
uv build
```

---

## 🗺️ Дорожная карта

Проект реализован в соответствии с планом [ROADMAP.md](ROADMAP.md) (**60 из 60 дней** полностью завершены):
- [x] **Этап 1 (Дни 1–12):** Структуры данных (`structures`)
- [x] **Этап 2 (Дни 13–24):** Алгоритмы и вычисления (`algorithms`)
- [x] **Этап 3 (Дни 25–36):** Декораторы и функциональные утилиты (`decorators`, `functional`)
- [x] **Этап 4 (Дни 37–48):** Обработка данных и строки (`data`, `strings`)
- [x] **Этап 5 (Дни 49–60):** Системные, CLI и файловые утилиты (`cli`, `system`)

---

## 📜 Лицензия

Проект распространяется под свободной лицензией [MIT](LICENSE).
Copyright (c) 2026 Denis Lopukhov (Gupkagrop).
