# Современные методы анализа данных и машинного обучения, БИ

## НИУ ВШЭ, 2025–2026 учебный год

    Растяпин Данил ББИ235  
    Игнатова Вероника ББИ235  
    Плаксин Глеб ББИ235  
    Мошенко Артём ББИ235  

---

## Проект

В рамках ГП2 мы собираем и анализируем информацию о видеоиграх с использованием API и скрэппинга. 

Цель — ...

---

## Источники


### API с IGDB

#### Контекст:
IGDB - это база данных игр, которая доступна по API.
**Почти тоже самое, что и IMDB, только для игр...**

Мы собираем данные через **5 эндпойнтов**:

|эндпойнт|что собираем|зачем|
|-|-|-|
|games|id, name, slug, first_release_date, platforms, genres, themes, game_modes, game_type, involved_companies, rating, rating_count, aggregated_rating, aggregated_rating_count, total_rating, total_rating_count, hypes, external_games, franchise, parent_game, remakes, remasters, storyline, summary, keywords|основная таблица — ядро датасета|
|involved_companies|company.name, company.id, game.name, game.id (фильтр: developer=true)|связка игра → студия-разработчик|
|keywords|id, name, slug|расшифровка keyword_id в человекочитаемые теги|
|game_time_to_beats|game_id, hastily, normally, completely, count|время прохождения (быстро / нормально / 100%)|
|alternative_names|comment, game, name|альтернативные названия (локализации, аббревиатуры)|

**Фильтр:** `rating != null & rating_count > 20` - берём только игры с достаточным количеством оценок.


- `aggregated_rating`, `rating`, `total_rating` - средние оценки
- `aggregated_rating_count`, `rating_count`, `total_rating_count` - количество оценок
- `hypes` - уровень ожидания
- `avg_time` - среднее время прохождения
- `time_without_side_quests` - время без побочных квестов
- `completely` - время для 100% прохождения
- `number_of_missions` - количество миссий
- `game_type` - тип игры
- `mode_*` - режимы: Single/Multi/Co-op/Battle Royale/MMO/Split screen
- `genre_*` - жанры: RPG, Shooter, Strategy, Adventure и др.
- `theme_*` - темы: Action, Fantasy, Horror, Open world и др.
- `price`, `currency` - цена и валюта
- `reviews_total_reviews` - количество отзывов
- `reviews_rating_value` - рейтинг отзывов
- `platform_*` (10 шт) - PC/Mac/Linux/PS/Xbox/Nintendo/Mobile и др.
- `available_platforms` - количество доступных платформ
- `developer`, `new_companies` - разработчики
- `franchise`, `parent_game` - франшиза/оригинал
- `remasters`, `remakes` - ремастеры/ремейки
- `first_release_date`, `year` - дата релиза
- `num_alt_names` - количество альтернативных названий
- `name`, `slug` - название (+ приведенные к общему виду)
- `keywords`, `tags`, `description` - описания игр
- `additional_info` - доп. информация