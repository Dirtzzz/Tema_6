# Тема 6. Базовые коллекции: словари, кортежи
Отчет по Теме #6 выполнил:
- Ильдейкин Антон Александрович
- ИНО ЗБ ПОАС-22-2

| Задание | Лаб_раб | Сам_раб |
| ------ | ------ | ------ |
| Задание 1 | - | + |
| Задание 2 | - | + |
| Задание 3 | - | + |
| Задание 4 | - | + |
| Задание 5 | - | + |
| Задание 6 | - | - |
| Задание 7 | - | - |
| Задание 8 | - | - |
| Задание 9 | - | - |
| Задание 10 | - | - |


Работу проверили:
- к.э.н., доцент Панов М.А.
## Самостоятельная работа №1
### При создании сайта у вас возникла потребность обрабатывать данные пользователя в странной форме, а потом переводить их в нужные вам форматы. Вы хотите принимать от пользователя последовательность чисел, разделенных пробелом, а после переформатировать эти данные в список и кортеж. Реализуйте вашу задумку. Для получения начальных данных используйте input(). Результатом программы будет выведенный список и кортеж из начальных данных.

```python
numbers = input('Введите числа: ')

lst = numbers.split()
tpl = tuple(lst)

print(lst, tpl, sep='\n')
```
### Результат:
![Меню](https://github.com/Dirtzzz/Tema_6/blob/main/6.1.png)

## Самостоятельная работа №2
### Николай знает, что кортежи являются неизменяемыми, но он очень упрямый и всегда хочет доказать, что он прав. Студент решил создать функцию, которая будет удалять первое появление определенного элемента из кортежа по значению и возвращать кортеж без него. Попробуйте повторить шедевр не признающего авторитеты начинающего программиста. Но учтите, что Николай не всегда уверен в наличии элемента в кортеже (в этом случае кортеж вернется функцией в исходном виде).
Входные данные:
(1, 2, 3), 1)
(1, 2, 3, 1, 2, 3, 4, 5, 2, 3, 4, 2, 4, 2), 3)
(2, 4, 6, 6, 4, 2), 9)
Ожидаемый результат:
(2, 3)
(1, 2, 1, 2, 3, 4, 5, 2, 3, 4, 2, 4, 2)
(2, 4, 6, 6, 4, 2)

```python
chisla = ['(1, 2, 3), 1)', '(1, 2, 3, 1, 2, 3, 4, 5, 2, 3, 4, 2, 4, 2), 3)', '(2, 4, 6, 6, 4, 2), 9)']


def remove_element(chi, lo):
    chisl = list(chi)
    if lo in chisl:
        chisl.remove(lo)
        return tuple(chisl)
    else:
        return chi


for chis in chisla:
    chi = tuple(map(int, chis[:-4].strip('()').split(',')))
    element = int(chi[-2:-1][0])
    new_chislo = remove_element(chi, element)
    print(new_chislo)
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_6/blob/main/6.2.png)

## Самостоятельная работа 3
### Ребята поспорили кто из них одним нажатием на numpad наберет больше повторяющихся цифр, но не понимают, как узнать победителя. Вам им нужно в этом помочь. Дана строка в виде случайной последовательности чисел от 0 до 9 (длина строки минимум 15 символов). Требуется создать словарь, который в качестве ключей будет принимать данные числа (т. е. ключи будут типом int), а в качестве значений - количество этих чисел в имеющейся последовательности. Для построения словаря создайте функцию, принимающую строку из цифр. Функция должна возвратить словарь из 3-х самых часто встречаемых чисел, также эти значения нужно вывести в порядке возрастания ключа.

```python
numpad = input('Нажмите ладонью на numpad один раз\n')


def count_numbers(string):
    nums_freq = {}

    for x in string:
        x = int(x)
        nums_freq[x] = nums_freq.get(x, 0) + 1

    sorted_nums_freq = sorted(nums_freq.items(), key=lambda item: item[1])
    top_tri = dict(sorted(sorted_nums_freq[-3:]))
    return top_tri


print(count_numbers(numpad))
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_6/blob/main/6.3..png)

## Самостоятельная работа 4
### Ваш хороший друг владеет офисом со входом по электронным картам, ему нужно чтобы вы написали программу, которая показывала в каком порядке сотрудники входили и выходили из офиса. Определение сотрудника происходит по id. Напишите функцию, которая на вход принимает кортеж и случайный элемент (id), его можно придумать самостоятельно. Требуется вернуть новый кортеж, начинающийся с первого появления элемента в нем и заканчивающийся вторым его появлением включительно.
Если элемента нет вовсе - вернуть пустой кортеж.
Если элемент встречается только один раз, то вернуть кортеж, который начинается с него и идет до конца исходного.
Входные данные:
(1, 2, 3), 8)
(1, 8, 3, 4, 8, 8, 9, 2), 8)
(1, 2, 8, 5, 1, 2, 9), 8)
Ожидаемый результат:
()
(8, 3, 4, 8)
(8, 5, 1, 2, 9)
```python
chisla = ['(1, 2, 3), 8)', '(1, 8, 3, 4, 8, 8, 9, 2), 8)', '(1, 2, 8, 5, 1, 2, 9), 8)']

def find_element(chis, element):
    if chis.count(element) > 0:
        start_index = chis.index(element)
        end_index = chis.index(element, start_index + 1) if chis.count(element) > 1 else ()
        return chis[start_index:end_index + 1] if end_index != () else chis[start_index:]
    else:
        return ()

for chi in chisla:
    chis = tuple(map(int, chi[1:-4].strip('()').split(',')))
    element = int(chi[-2])
    new_chislo = find_element(chis, element)
    print(new_chislo)
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_6/blob/main/6.4..png)

## Самостоятельная работа 5
### Самостоятельно придумайте и решите задачу, в которой будут обязательно использоваться кортеж или список. Проведите минимум три теста для проверки работоспособности вашей задачи.
Задача: В магазине техники есть множество позиций. В базе данных магазина занесена информация о каждой позиции на складе, в том числе и о цене. Необходимо посчитать стоимость всей техники на складе.

```python
hardware_info = [('Ноутбук acer', 10), ('Системные блок zalman', 30), ('Монитор @lg', 25), ('Телефон xiaomi', 53)]
hardware_prices = {'Ноутбук acer': 50000, 'Системные блок zalman': 129999, 'Монитор @lg': 10000, 'Телефон xiaomi': 30000}

total_price = 0

for hardware, counts in hardware_info:
    hardware_price = hardware_prices[hardware]
    total_price += counts * hardware_price

print(f"Общая стоимость всей техники: {total_price} руб.")
```

### Результат:
![Меню](https://github.com/Dirtzzz/Tema_6/blob/main/6.5.png)
