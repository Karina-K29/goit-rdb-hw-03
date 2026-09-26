# goit-rdb-hw-03 — SQL: завантаження, типізація, аудит якості та EDA

## Датасет
**NYC TLC Yellow Taxi Trip Records** — записи поїздок жовтого таксі Нью-Йорка.

- Офіційне джерело: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- Файл: `yellow_tripdata_2026-07.parquet` (липень 2026)
  https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2026-07.parquet
- Словник даних: https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf

## Як сформовано вибірку
1. Notebook сам завантажує місячний Parquet-файл з офіційного посилання TLC (весь рік не завантажується).
2. Залишаються 12 колонок: `VendorID`, `tpep_pickup_datetime`, `tpep_dropoff_datetime`, `passenger_count`, `trip_distance`, `PULocationID`, `DOLocationID`, `payment_type`, `fare_amount`, `tip_amount`, `total_amount`, `store_and_fwd_flag`.
3. Беруться перші **100 000 рядків** (`head(100_000)`) і зберігаються у `data/hw3_taxi_sample.csv`.
4. CSV завантажується в PostgreSQL через `COPY FROM STDIN` у staging-таблицю `hw3_data_staging` (усі колонки `TEXT`), потім очищується і переноситься в типізовану таблицю `hw3_taxi_trips` через `INSERT INTO ... SELECT`.

**Кількість рядків:** 100 000 у staging і 100 000 у clean-таблиці.

## Як запустити
1. Відкрити `hw3_sql_Kostiuk.ipynb` у Google Colab.
2. `Runtime → Restart session and run all`.

PostgreSQL встановлюється і запускається прямо в Colab (`apt-get install postgresql`), SQL-клітинки працюють через `jupysql`, дані завантажуються автоматично.

## Структура репозиторію
```
goit-rdb-hw-03/
├── README.md
├── hw3_sql_Kostiuk.ipynb
└── data/
    └── hw3_taxi_sample.csv
```
