# Лабораторная работа №2

> Кэш - промежуточный буфер с быстрым доступом, содержащий информацию, которая может быть запрошена с наибольшей вероятностью. Доступ к данным в кэше осуществляется быстрее, чем выборка исходных данных из более медленной памяти или удаленного источника, однако её объём существенно ограничен по сравнению с хранилищем исходных данных.

### Задача

Для каждого из вариантов проходов (*прямой*, *обратный* и *случайный*) целочисленного массива 
провести исследование зависимости времени от размера.

Каждое исследование включает в себя серию эксперементов c определенными размерами.

Количество экспериментов в серии определяется следующим образом:

```cpp
1/2 * cache_sizes['1'] < 2^x < 2^(x+1) < ... < 2^(x+n) < 3/2 * cache_sizes['max']
```

### Пример

В примере ниже показано, что для процессора с тремя уровнями кэша (`2mb`, `4mb`, `8mb`)
необходимо провести серию из 5 эксперементов.

```cpp
cache_size['1'] = 2 mb;
cache_size['2'] = 4 mb;
cache_size['3'] = 8 mb;

// 1mb < 2mb < 4mb < 8mb < 12mb
```

### Эксперимент

Каждый эксперемент состоит из 3 шагов:

```cpp
1. Создание буфера
2. Прогревание кэша
// <-- время начала эксперемнта
3. Циклический проход (1000 итераций)
// <-- время окончание эксперемента
```

#### Шаг 1

Инициализация буфера может происходит, как с помощью чтения данных из файла в выделенную область памяти,
так и с помощью случайного заполнения с использованием генератора случайных чисел.

#### Шаг 2

Данный шаг необходимо выполнить для получения репрезентативных данных, т.к. кэш-память еще не заполнена.

#### Шаг 3

Для получения времени обхода от размера массива процедуру прохода необходимо многократно повторить (порядка 1000 раз).

### Результаты

Ниже представлен формат и пример отчета:

```yaml
investigation:                                       |  investigaion:
  travel_variant: <вариант_прохода>                  |    travel_order: "direction"
  experiments:                                       |    experiments:
  - experiment:                                      |    - experiment:
      number:                                        |        number: 1
      input_data:                                    |        input_data:
        buffer_size: <размер_буфера>                 |          buffer_size: "1mb"
      results:                                       |        results:
        duration: <продолжительность>                |          duration: "1ns"
  - experiment:                                      |    - experiment:
      number: <номер_эксперимента>                   |        number: 2
      input_data:                                    |        input_data:
        buffer_size: <размер_буфера>                 |          buffer_size: "2mb"
      results:                                       |        results:
        duration: <продолжительность>                |          duration: "2ns"
                                                     |
investigation:                                       |  investigation:
...                                                  |  ...
```

⚠️ В отчет также необходимо добавить общий график с результатами всех исследований. ⚠️

#  Результат
[![Build Status](https://travis-ci.org/Verestchagin/lab-02-cache.svg?branch=master)](https://travis-ci.org/Verestchagin/lab-02-cache)

### Графики ###
[direct](http://yotx.ru/#!1/3_h/sH@1sHBwcH@0YM4X9t/2j/YP9g309Kre1vnIJ4oC3E2eXuxtYOjAfb2TmA7W7snJ3ytk5BB5dbuxtnWzu8ix3YGehsd2PrYAfEOz2FnV5c7m7sHIBgvK2L0zPE6dbuBujg8pS3c4o43TkF7W7Ati53eGc7lzDQGWJ3f2efRMNu7JwyHk@3GI9blxe7@1v7@wA=)

[reverse](http://yotx.ru/#!1/3_h/sH@1sHBwcH@0YM4X9t/2j/YP9g309Kre1vnIJ4oIODs4vdja0dGA92cQoD7W7snJ3yts4utxCXuxtnWzu8iy3EFgK2u7F1sAPine5cHOxc7G7sHIBgvK2dsx3EzsXuBujg8pS3c3Z2cXZxsLsB27rc4Z3t7BwgLkG7@zv7JBp2Y@eU8Xi6xXjcurzY3d/a3wcF)

[random](http://yotx.ru/#!1/3_h/sH@1sHBwcH@0YM4X9t/2j/YP9g309Kre1vnIJ4WxcHF1sHO7sbWzsw3s7pzsXpKWx3Y@fslHe2s4M42DrY3Tjb2uFtHSBgW6Cdy92NrYMdEG9nC7R1trO1u7FzAILxQDug060t2M7uBujg8pR3uXO6dXoK29rdgG1d7vC2YAcw0AFs63J3f2efRMNu7JwyHk@3GI9blxe7@1v7@wA=)

[compare](http://yotx.ru/#!1/3_h/sH@1sHBwcH@0YM4X9t/2j/YP9g309Kre1vnIJ4WxcHF1sHO7sbWzsw3s7pzsXpKWx3Y@fslHe2s4M42DrY3Tjb2uFtHSBgW6Cdy92NrYMdEG9nC7R1trO1u7FzAILxQDug060t2M7uBujg8pR3uXO6dXoK29rdgG1d7vC2YAcw0AFs63J3f2efRMNubMEQjMcDxuPB7v7W/v7GKYgHOjg4u9jd2NqB8WAXpzDQ7sbO2Slv6@xyC3G5u3G2tcO72EJsIWC7G1sHOyDe6c7Fwc7F7sbOAQjG29o520HsXOxugA4uT3k7Z2cXZxcHuxuwrcsd3tnOzgHiErS7v7NPomE3QAeMxx3QFuMRdLC7v7O/v3EK4oG2EGeXuxtbOzAebGfnALa7sXN2yts6BR1cbu1unG3t8C52YGegs92NrYMdEO/0FHZ6cbm7sXMAgvG2Lk7PEKdbuxugg8tT3s4p4nTnFLS7Adu63OGd7VzCQGeI3f2dfRINu7Fzyng83WI8bl1e7O5v7e8DBg==)

| Number      | Buffer size | Direct Time | Reverse Time | Random Time |
| ----------- |------------------| -----|
| 1           | выровнен вправо    | $1600 |
| 2           | выровнен по центру |   $12 |
| 3           | прикольные         |    $1 |
