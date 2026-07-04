# Vector Safety Filter

Embedded-система фильтрации небезопасного контента на онлайн-доске для рисования

[![Python](https://img.shields.io/badge/Python-3.14-blue?logo=python)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-orange?logo=pytorch)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## О проекте

Vector Safety Filter — прототип системы, анализирующей векторные рисунки и 
классифицирующей их по признаку безопасности для детской аудитории.

Система работает с векторными данными (последовательностями координат штрихов):
- Анализ в реальном времени без потери качества
- Сжатое хранение данных (до 97% экономии)
- Распознавание геометрических паттернов

Возможности:
- Сбор векторных рисунков с ручной разметкой (safe/unsafe)
- Анализ датасета с визуализацией
- Аугментация данных (7 видов трансформаций)
- Обучение гибридной CNN + LSTM нейронной сети
- Классификация рисунков в реальном времени
- Визуализация метрик и ошибок

---

## Архитектура

Три модуля:
- Сбор данных (Tkinter + SQLite)
- Обучение (Jupyter + PyTorch)
- Инференс (Tkinter + PyTorch)

Технологии:
- Python 3.14
- PyTorch
- CNN + LSTM
- Tkinter
- SQLite
- Matplotlib, Seaborn
- Jupyter Notebook

---

## Быстрый старт

1. Установка зависимостей:

git clone https://github.com/AstroPolly/vector-safety-filter.git
cd vector-safety-filter

python -m venv .venv
.venv\Scripts\Activate.ps1  # Windows PowerShell
pip install -r requirements.txt

2. Сбор данных:

python collector_app.py

Рисуйте, выбирайте категорию (safe/unsafe), сохраняйте.

3. Обучение модели:

jupyter notebook learn.ipynb

Выполняйте ячейки по порядку. Модель сохранится в best_model.pth

4. Проверка рисунков:

python inference_app.py

Нарисуйте и нажмите "ПРОВЕРИТЬ БЕЗОПАСНОСТЬ"

---

## Архитектура нейросети

Вход: [batch, 20 штрихов, 50 точек, 2 координаты]

CNN (признаки штрихов)
  Conv1d(2→32) + ReLU + MaxPool
  Conv1d(32→64) + ReLU + MaxPool

LSTM (последовательность штрихов)
  2 слоя, hidden_size=64

Классификатор
  Linear(64→32) + ReLU + Dropout
  Linear(32→1) + Sigmoid

Выход: вероятность unsafe [0, 1]

Параметры: ~1.2 млн
Время инференса: 50-200 мс

---

## Аугментация данных

7 видов трансформаций:
- Поворот на 90, 180, 270 (30%)
- Отражение по горизонтали (25%)
- Отражение по вертикали (25%)
- Добавление шума (40%)
- Удаление штрихов (20%)
- Удаление точек (30%)
- Масштабирование 0.7-1.3 (20%)

---


## Лицензия

MIT License

---

## Автор

Жирнова Полина
Студентка МТУСИ
Производственная практика 2026

---

[GitHub](https://github.com/AstroPolly/vector-ai)