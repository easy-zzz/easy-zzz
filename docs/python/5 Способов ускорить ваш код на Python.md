---
дата создания: 2023-04-07 17:07
дата изменений: пятница 7-го апреля 2023 17:07:43
---

# 5 Способов ускорить ваш код на Python

> Там, где есть милосердие и мудрость, нет ни страха, ни невежества.
> — <cite>Francis of Assisi</cite>

## Используйте встроенные функции

```python
import time 
```

```python
# Медленный:
 
start = time.time() 

word_list = ['Ways', 'to', 'Make', 'Your', 'Python', 'Code', 'Faster'] 
new_list = [] 

for word in word_list: 
    new_list.append(word.capitalize())
```

```python
print(time.time() - start, "секунд")
```

```python
# бытрый

start = time.time() 
 
word_list = ['Ways', 'to', 'Make', 'Your', 'Python', 'Code', 'Faster']  
new_list = list(map(str.capitalize, word_list)) 
 
print(time.time() - start, "секунд") 
```
## Объединение строк против join()

## Быстрее создавайте списки и словари

## f-строки

## Список понятий