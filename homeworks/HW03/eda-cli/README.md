# S03 – eda_cli: мини-EDA для CSV

Небольшое CLI-приложение для базового анализа CSV-файлов.
Используется в рамках Семинара 03 курса «Инженерия ИИ».

## Требования

- Python 3.11+
- [uv](https://docs.astral.sh/uv/) установлен в систему

## Инициализация проекта

В корне проекта (S03):

```bash
uv sync
```

Эта команда:

- создаст виртуальное окружение `.venv`;
- установит зависимости из `pyproject.toml`;
- установит сам проект `eda-cli` в окружение.

## Запуск CLI

### Краткий обзор

```bash
uv run eda-cli overview data/example.csv
```

Параметры:

- `--sep` – разделитель (по умолчанию `,`);
- `--encoding` – кодировка (по умолчанию `utf-8`).


- `--title TEXT` — заголовок отчёта в Markdown (по умолчанию: "EDA-отчёт"). 
- `--min-missing-share FLOAT` — порог доли пропусков (от 0 до 1), выше которого колонка считается проблемной (по умолчанию: 0.5).

Пример отчета с новыми параметрами
```bash
uv run eda-cli report --title UF --min-missing-share 0.6 data/example.csv
Отчёт сгенерирован в каталоге: reports
- Основной markdown: reports\report.md
- Табличные файлы: summary.csv, missing.csv, correlation.csv, top_categories/*.csv
- Графики: hist_*.png, missing_matrix.png, correlation_heatmap.png
```

### Полный EDA-отчёт

```bash
uv run eda-cli report data/example.csv --out-dir reports
```

В результате в каталоге `reports/` появятся:

- `report.md` – основной отчёт в Markdown;
- `summary.csv` – таблица по колонкам;
- `missing.csv` – пропуски по колонкам;
- `correlation.csv` – корреляционная матрица (если есть числовые признаки);
- `top_categories/*.csv` – top-k категорий по строковым признакам;
- `hist_*.png` – гистограммы числовых колонок;
- `missing_matrix.png` – визуализация пропусков;
- `correlation_heatmap.png` – тепловая карта корреляций.

## Тесты

```bash
uv run pytest -q
```
