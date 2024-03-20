1. Постройте график
Назовите график
Сделайте именование оси x и оси y
Сделайте выводы

1.1. Скачать данные по ссылке https://gbcdn.mrgcdn.ru/uploads/asset/4266730/attachment/08ec55854637add5247d22396d0f7456.csv

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np


df = pd.read_csv('kc_house_data.csv', sep=',')
df

2. Изучите стоимости недвижимости
plt.figure(figsize=(6, 6))
plt.hist(df['price'])
plt.title('Распределение стоимости недвижимости')
plt.xlabel('Стоимость')
plt.ylabel('Количество');

![image](https://github.com/Repin23/1.1/assets/139049242/045d3b90-58f0-4c67-a941-9f80cf36cf01)

3. Изучите рапспределение квадратуры жлилой
plt.figure(figsize=(6, 8))
sns.histplot(df['sqft_living'], bins=20)
plt.title('Распределение квадратуры жилой')
plt.xlabel('Кв. метры жилые')
plt.ylabel('Количество');


![image](https://github.com/Repin23/1.1/assets/139049242/a4acee21-58f4-4141-84f3-f5ff124b22e5)

4. Изучите распредление года постройки
   
plt.figure(figsize=(6, 8))
sns.histplot(df['yr_built'], bins=30)
plt.title('Распределение года постройки')
plt.xlabel('Год постройки')
plt.ylabel('Количество');

![image](https://github.com/Repin23/1.1/assets/139049242/2dc8c0a2-85a1-40bb-a0ca-a177d1be92c4)

5. Изучите распределение домов от наличия вида на набережную
Постройте график
Сделайте выводы

data = df['waterfront'].value_counts()
plt.figure(figsize=(6, 4))
plt.pie(data, autopct='%1.1f%%')
plt.legend(['no', 'yes']);

![image](https://github.com/Repin23/1.1/assets/139049242/7b3ac66d-0752-4f60-be5c-8d483e0fb80f)

6. Изучите распределение этажей домов
   
data = df['floors'].value_counts()
plt.figure(figsize=(6, 4))
plt.pie(data, autopct='%1.1f%%', labels=data.index)
plt.title('Количество этажей');

![image](https://github.com/Repin23/1.1/assets/139049242/31f4f408-b624-4030-9a48-5473ca84bbd0)

Изучите распределение состояния домов

data = df['condition'].value_counts()

plt.figure(figsize=(6, 4))
plt.pie(data, autopct='%1.1f%%', labels=data.index);

![image](https://github.com/Repin23/1.1/assets/139049242/8813933d-adf3-4102-8b75-a2555a56abdd)

Исследуйте, какие характеристики недвижимости влияют на стоимость недвижимости, с применением не менее 5 диаграмм из урока. 
Анализ сделайте в формате storytelling: дополнить каждый график письменными выводами и наблюдениями.

corr_matrix = df.corr(numeric_only=True)
corr_matrix = np.round(corr_matrix, 1)
corr_matrix[np.abs(corr_matrix) < 0.3] = 0
corr_matrix

plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, linewidths=.5, cmap='coolwarm');

![image](https://github.com/Repin23/1.1/assets/139049242/fd06b823-316e-47cc-87a9-24b647b8e5b0)

sns.jointplot(x=df['price'], y=df['sqft_living'], kind='reg');

![image](https://github.com/Repin23/1.1/assets/139049242/6b853107-78e9-4c35-aeb8-5be7c6754c09)

Чекм больше жил площадь- тем дороже квартира
sns.jointplot(x=df['price'], y=df['grade'], kind='reg');

![image](https://github.com/Repin23/1.1/assets/139049242/e12f1a57-3fb4-4992-94e6-5367767cd5aa)

Чем выше качество материалов и дизайн дома, тем стоимость дороже
sns.boxplot(x=df['price'], y=df['grade'].astype('str'), whis=1.5);
plt.xlabel('price')
plt.ylabel('grade')
plt.title('Distribution of price by grade');

![image](https://github.com/Repin23/1.1/assets/139049242/7265615d-4b25-4ea5-8c95-af2129ff00ba)

Наибольшая стоимость у домов 13

sns.boxplot(x=df['price'], y=df['floors'].astype('str'), whis=1.5);
plt.xlabel('price')
plt.ylabel('floors')
plt.title('Distribution of price by floors');

![image](https://github.com/Repin23/1.1/assets/139049242/251e317a-a87f-4069-8872-79d164974821)

Наибольшая стоимость у домов с эт 2.5
sns.boxplot(x=df['price'], y=df['view'].astype('str'), whis=1.5);
plt.xlabel('price')
plt.ylabel('view')
plt.title('Distribution of price by view');

![image](https://github.com/Repin23/1.1/assets/139049242/f7cc71fc-4866-4dfb-873c-737f9f5af121)

Наибольшая стоимость дома с оценкой вида 4







































