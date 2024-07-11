В ячейке ниже представлен код генерирующий DataFrame, которая состоит всего из 1 столбца. Ваша задача перевести его в one hot вид. Сможете ли вы это сделать без get_dummies?

import random
lst = ['robot'] * 10
lst += ['human'] * 10
random.shuffle(lst)
data = pd.DataFrame({'whoAmI':lst})

Да, можно выполнить преобразование в one hot вид без использования функции get_dummies из библиотеки pandas. Для этого можно воспользоваться методом pd.DataFrame для создания нового DataFrame, где каждый столбец будет представлять собой отдельную категорию, а значения будут 0 или 1 в зависимости от того, соответствует ли строка данной категории.

Вот пример кода для выполнения этой задачи:

import pandas as pd
import random
# Генерация исходного DataFrame
lst = ['robot'] * 10
lst += ['human'] * 10
random.shuffle(lst)
data = pd.DataFrame({'whoAmI': lst})
# Преобразование в one hot вид
unique_values = data['whoAmI'].unique()
# Создаем пустой DataFrame для one hot encoding
one_hot_df = pd.DataFrame()
# Заполняем DataFrame one hot encoding данными
for value in unique_values:
    one_hot_df[value] = (data['whoAmI'] == value).astype(int)
# Добавляем one hot encoding столбцы к исходному DataFrame
data = pd.concat([data, one_hot_df], axis=1)
print(data)

Этот код выполняет следующие шаги:
Генерирует исходный DataFrame.
Находит уникальные значения в столбце whoAmI.
Создает новый DataFrame one_hot_df, где каждый столбец соответствует уникальному значению.
Заполняет новый DataFrame, устанавливая значения 1, если строка соответствует данной категории, и 0 в противном случае.
Объединяет исходный DataFrame с новым DataFrame one_hot_df.
В результате получится DataFrame с оригинальными данными и добавленными столбцами one hot encoding:
python
Копировать код
   whoAmI  robot  human
0   robot      1      0
1   human      0      1
2   robot      1      0
3   robot      1      0
4   human      0      1
...

