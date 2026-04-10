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

