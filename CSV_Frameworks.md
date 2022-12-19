### 1. Открыть файл:
import csv
import pandas as pd

df = pd.read_csv('Filename.csv', sep=';', encoding="cp1251")
df.head()

---

### 2. Сделать гистограмму по датафрейиу из предыдущего пункта:
import plotly.express as px

res = px.bar(df, x = 'Финансовый рейтинг', y = 'Name', title = 'Финансовый рейтинг', template = 'simple_white')

res.update_layout(yaxis_title = '',
                 xaxis_title = '',
                 title = {'font':dict(size = 25),
                         'x':0.5})
res.show()

---

### 3. Создать новый фреймворк из столбцов '_IDBank' и 'Name' существующего df:
df_new = df[['_IDBank', 'Name']]

---

### 4. Переименовать колонку с имени Name в имя Банк:
df_new = df_new.rename(columns={'Name': 'Банк'})

---

### 5. Соединить 2 фреймворка:
df_merged = pd.merge(df1, df2)

---

### 6. Изменить тип данных столбца в датафрейме:
df['Дата создания'] = pd.to_datetime(df['Дата создания'])

---

### 7. Вывести сегодняшнюю дату:
from datetime import date
type(date.today())

---

### 8. Создать столбец с сегодняшней датой и перевести его в тип данных datetime64:
df['Дата_сегодня'] = date.today()
df['Дата_сегодня'] = df['Дата_сегодня'].astype('datetime64')

---

### 9. Информация о типах данных колонок датафрейма:
df.info()

---

### 10. Вывести разницу между датами в месяцах:
import numpy as np

df['Gap_months'] = df['Дата_сегодня'] - df['Дата создания']
df['Gap_months'] = df['Gap_months'] / np.timedelta64(1, 'M')
df['Gap_months'] = df['Gap_months']
df.head()

---

### 11. Заменить отдельные значения (в данном случае '<0') на ноль (можно на любое другое значение или число, если позволяет тип):
df['Срок_вклада_в_месяцах_new'] = df['Срок_вклада_в_месяцах_new'].replace('<0', 0)

---

### 12. Сохранить в отдельный датафрейм строки, удовлетворяющие условию:
df_res = df[df['Activ'] < 0]
df_res

---

### 13. Сгруппировать, сортировать, для красивого вывода поместить в датафрейм, переименовать колонку:
df_final = pd.DataFrame(df_res.groupby('Банк').count()['_IDVklad'].sort_values(ascending=True))
df_final = df_final.rename(columns={'_IDVklad' : 'Количество вкладов'})
df_final

---

### 14. Сохранить результирующий датафрейм в файл .csv:
df_final.to_csv('Количество активных вкладов у банков.csv')