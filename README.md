# Recipe_Recommender
# PySpark Recipe Recommender — Debugged Version

This folder contains corrected versions of the original Recipe Recommender / EDA notebooks.

## Recommended file

Use **`improved_final_submission_complete.ipynb`** if you want the entire assignment in one notebook.

## Corrected notebooks

- `improved_data_reading.ipynb`
- `improved_typecasting.ipynb`
- `improved_feature_extraction.ipynb`
- `improved_eda.ipynb`
- `improved_final_submission_part1.ipynb`
- `improved_final_submission_part2.ipynb`
- `improved_final_submission_complete.ipynb`

## Data location

By default, the notebooks expect:

```text
./data/RAW_recipes.csv
./data/RAW_interactions.csv
```

You can set another local or S3 location with environment variables:

```bash
export RECIPE_DATA_ROOT=/path/to/data
```

or

```bash
export RECIPE_DATA_ROOT=s3a://your-real-bucket/path
```

You can also set the two files independently:

```bash
export RECIPES_PATH=/path/RAW_recipes.csv
export INTERACTIONS_PATH=/path/RAW_interactions.csv
```

## Main fixes

1. Added all missing imports (`FloatType` equivalent through `types`, `IntegerType`, and `Window`).
2. Removed brittle `inferSchema` assumptions and explicitly cast required numeric fields.
3. Replaced the placeholder-only S3 path with configurable local/S3 paths.
4. Correctly removed `[` / `]` before parsing the `nutrition` list.
5. Avoided division by zero when creating per-100-calorie nutrient features.
6. Correctly converted tag strings such as `['tag-a', 'tag-b']` to `array<string>`.
7. Rebuilt the recipe/interactions join after recipe transformations so `combined_df` contains transformed tags/features.
8. Replaced invalid `StringIndexer + OneHotEncoder` on tag arrays with binary `CountVectorizer` multi-hot encoding.
9. Fixed invalid `explode('tags')` usage by ensuring tags are arrays first.
10. Replaced Unix timestamp arithmetic with `to_date` + `datediff` for `days_between`.
11. Created `days_between` inside the EDA notebook before plotting it.
12. Removed full-dataset `combined_df.toPandas()` and converted only bounded/aggregated plotting data.
13. Completed the previously incomplete final-submission Part 2 notebook.
14. Added a single complete notebook containing Tasks 01–09.

## Requirements

```bash
pip install pyspark pandas matplotlib seaborn jupyter
```

A Java installation compatible with your Spark version is also required.

