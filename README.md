# 📊 Email & Account Activity Report (SQL + Looker Studio)

## 🔍 Мета проєкту

Побудувати аналітичний SQL-запит для оцінки динаміки створення акаунтів та ефективності email-розсилок на основі e-commerce бази даних у **BigQuery**. Додатково створено **візуалізацію в Looker Studio** на базі згенерованих даних.

---

## 🧩 Опис логіки запиту

Запит складається з кількох логічних частин, реалізованих через CTE:

### 1. `account_metrics`
- Рахує кількість створених акаунтів (`account_cnt`) у розрізі:
  - `date`
  - `country`
  - `send_interval`
  - `is_verified`
  - `is_unsubscribed`

### 2. `email_metrics`
- Рахує:
  - `sent_msg` — відправлені листи
  - `open_msg` — відкриті листи
  - `visit_msg` — переходи по листах
- У тих самих розрізах, що й акаунти.

### 3. `combined_metrics`
- Об'єднує акаунти та емейли за допомогою `UNION ALL`.

### 4. `aggregated_metrics`
- Підсумовує дані та обчислює:
  - `total_country_account_cnt` — загальна кількість акаунтів у країні
  - `total_country_sent_cnt` — загальна кількість листів

### 5. `ranked_metrics`
- Ранжує країни за допомогою функцій-вікон:
  - `rank_total_country_account_cnt`
  - `rank_total_country_sent_cnt`

### 🎯 Фінальна вибірка
- Виводяться лише країни, які входять у ТОП-10 за акаунтами або емейлами.
- 
