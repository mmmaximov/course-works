# Kaggle Competition: Feature Engineering & Ансамбли
## Соревнование [Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic/overview)
- 242 из 1694 место на момент написания
- $\text{Classification accuracy} = 0.80827$
- Топ 15% (~14.3%)
<img width="1151" height="239" alt="Screenshot 2026-08-04 074800" src="https://github.com/user-attachments/assets/406f70bd-7870-4fb6-80fc-b474b83ca5e7" />

Файл [submission.csv](https://github.com/mmmaximov/course-works/blob/main/dz2/submission.csv), который дал финальный результат
## Краткое описание подхода


## Что сработало лучше всего
- CatBoost с нативной обработкой категорий - главный вклад (+~0.016 к baseline).
- Feature engineering: разделение Luxury/Regular трат, групповое заполнение пропусков, флаги пропусков.
- Правильная валидация (`StratifiedGroupKFold` + accuracy): CV коррелирует с LB.
- Early stopping + больше итераций; seed-бэггинг для стабильности.

## Что не сработало
- Ансамбль/блендинг - модели скоррелированы на 0.98, прироста нет.
- Линейная модель в ансамбле - корреляция всё равно ~0.93.
- Фамильные фичи (Surname) - добавляли шум, CV падал.
- Подбор порога классификации - 0.5 оптимален (баланс классов).
- Агрессивный тюнинг accuracy - метрика шумная, прирост в пределах шума.

## Инструкция по воспроизведению результата

1. Открыть [страницу соревнования](https://www.kaggle.com/competitions/spaceship-titanic) → **Code** → **New Notebook**.
2. В панели справа **Add Input** → добавить датасет соревнования Spaceship Titanic
   (данные окажутся по пути `/kaggle/input/competitions/spaceship-titanic/`).
3. Загрузить `SpaceshipTitanicFinal` (File → Import Notebook) или скопировать ячейки.
4. Убедиться, что включён интернет/ускоритель не требуется — задача на CPU.
5. **Run All**. Полный прогон занимает ~10 минут.
6. Файл `submission.csv` создаётся в последней секции (9) в `/kaggle/working/`.
7. **Submit** этого файла на соревнование → результат появится на public LB.
