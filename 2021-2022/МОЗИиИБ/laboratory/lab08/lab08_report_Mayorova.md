---
# Front matter
title: "Отчёт по лабораторной работе №8"
author:
  - "Студент: Майорова О.А., НФИмд-02-21"
  - "Преподаватель: д.ф.-м.н. Кулябов Д.С."
date: "Москва 2021"

# Generic otions
lang: ru-RU
toc-title: "Содержание"

# Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt

## I18n
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
  
## Misc options
indent: true
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
  - \usepackage{titling}
  - \setlength{\droptitle}{-9em}
  - \pretitle{\begin{center}
      \textbf{РОССИЙСКИЙ УНИВЕРСИТЕТ ДРУЖБЫ НАРОДОВ}\\
      \textbf{Факультет физико-математических и естественных наук}\\
      \textbf{Кафедра прикладной информатики и теории вероятностей}
      \vspace{9cm}
      \LARGE\\}
  - \posttitle{\vskip 1em \large \emph{\textit{Дисциплина$:$ Математические основы защиты информации и информационной безопасности}} \end{center}}
  - \preauthor{\vskip 3em \begin{flushright} \large \begin{tabular}[t]{c}}
  - \postauthor{\end{tabular}\par\end{flushright} \vfill \vskip 5em}
---

# Цель работы
Цель: Ознакомиться с целочисленной арифметикой многократной точности.


# Задание
Программно реализовать алгоритмы: сложения неотрицательных целых чисел, вычитания неотрицательных целых чисел, 
умножения неотрицательных целых чисел, быстрый столбик и деления многоразрядных целых чисел.

# Теоретическое введение
Длинная арифметика — выполняемые с помощью вычислительной машины арифметические операции
(сложение, вычитание, умножение, деление, возведение в степень, элементарные функции) над числами,
разрядность которых превышает длину машинного слова данной вычислительной машины.
Эти операции реализуются не аппаратно, а программно, с использованием базовых аппаратных средств работы с числами меньших порядков.

Длинная арифметика применяется в следующих областях:

- составление кода для процессоров (микроконтроллеров) низкой разрядности. Например, микроконтроллеры серии AVR имеют АЦП с разрядностью 10 бит и регистры с разрядностью 8 бит. Этого недостаточно для обработки информации с АЦП; без длинной арифметики не обойтись;
- криптография. Большинство систем подписывания и шифрования данных используют целочисленную арифметику по модулю m, где m — очень большое натуральное число, не обязательно простое. Например, при реализации метода шифрования RSA, криптосистемы Рабина или схемы Эль-Гамаля требуется обеспечить точность результатов умножения и возведения в степень порядка 10309;
- математическое. Результат вычисления на бумаге должен совпадать с результатом работы компьютера с точностью до последнего разряда. В частности, калькулятор Windows (начиная с Windows 95) проводит четыре арифметических действия с намного большей точностью, чем позволяет процессор x86. Для научных и инженерных расчётов длинная арифметика применяется редко, так как ошибки во входных данных обычно намного больше, чем ошибки округления [@wiki].


Будем считать, что число в $b$-ичной системе счисления, $b$ - натуральное число, $b \ge 2$. Натуральное $n$-разрядное число число будем записывать в виде: $u = u_1u_2...u_n$.
При работе с большими целыми числами знак такого числа удобно хранит в отдельной переменной. Например, при умножении двух чисел, знак произведения
вычисляется отдельно [@lab].

# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбран язык Python. Далее реализуем представленные алгоритмы в виде функции в соответствии с описанием из задания к лабораторной работе.

Сначала реализуем алгоритм сложения неотрицательных целых чисел:
```
def alg1(u, v, n, b):
    u = [int(x) for x in str(u)]
    v = [int(x) for x in str(v)]
    w = []
    j = n
    k = 0
    
    while j > 0:
        w.append((u[j-1] + v[j-1] + k) % b)
        k = (u[j-1] + v[j-1] + k) // b
        j -= 1
        
    w.append(k)
    w.reverse()
    
    return int(''.join(str(x) for x in w))
```
Результатом запуска функции будет рис. [-@fig:alg1res].

![Проверка функции](image/alg1res.png){ #fig:alg1res width=100% }

Далее реализуем алгоритм вычитания неотрицательных целых чисел:
```
def alg2(u, v, n, b):
    u = [int(x) for x in str(u)]
    v = [int(x) for x in str(v)]
    w = []
    j = n
    k = 0
    
    while j > 0:
        w.append((u[j-1] - v[j-1] + k) % b)
        k = (u[j-1] - v[j-1] + k) // b
        j -= 1
        
    w.reverse()
    
    return int(''.join(str(x) for x in w))
```
Результатом запуска функции будет рис. [-@fig:alg2res].

![Проверка функции](image/alg2res.png){ #fig:alg2res width=100% }

Далее реализуем алгоритм умножения неотрицательных целых чисел:
```
def alg3(u, v, b):
    u = [int(x) for x in str(u)]
    v = [int(x) for x in str(v)]
    w = [0] * len(u + v)
    j = len(v)
    k = 0
    
    while j > 0:
        if v[j-1] == 0:
            w[j-1] = 0
        else:
            i = len(u)
            k = 0
            while i > 0:
                t = u[i-1]*v[j-1] + w[i+j-1] + k
                w[i+j-1] = t % b
                k = t // b
                i -= 1
            w[j-1] = k
        j -= 1
    
    return int(''.join(str(x) for x in w))
```
Результатом запуска функции будет рис. [-@fig:alg3res].

![Проверка функции](image/alg3res.png){ #fig:alg3res width=100% }

Далее реализуем алгоритм быстрый столбик:
```
def alg4(u, v, b):
    u = [int(x) for x in str(u)]
    v = [int(x) for x in str(v)]
    w = [0] * len(u + v)
    t = 0
    n = len(u)
    m = len(v)
    
    j = -n + 1
    for s in range(m + n):
        if s >= (m + n) // 2:
            r1 = j
            r2 = s+1-j
        else:
            r1 = 0
            r2 = s+1
            
        for i in range(r1, r2):
            t += u[n-i-1] * v[m-s+i-1]
            
        j += 1
        w[m+n-s-1] = t % b
        t = t // b
    
    return int(''.join(str(x) for x in w))
```
Результатом запуска функции будет рис. [-@fig:alg4res].

![Проверка функции](image/alg4res.png){ #fig:alg4res width=100% }

Наконец, реализуем алгоритм деления многоразрядных целых чисел:
```
def alg5(u, v, b):
    n = len(str(u))
    t = len(str(v))
    q = [0] * (n - t + 1)

    while u >= v*b**(n-t):
        q[n-t] += 1
        u -= v*b**(n-t)

    ul = [int(x) for x in str(u)]
    vl = [int(x) for x in str(v)]
    
    i = n
    while i > t:
        if ul[i] >= vl[t]:
            q[i-t-1] = b-1
        else:
            q[i-t-1] = (ul[i]*b + ul[i-1])/vl[t]
        
        while q[i-t-1]*(vl[t]*b + vl[t-1]) > ul[i] * b**2 + ul[i-1]*b + ul[i-2]:
            q[i-t-1] -= 1
            
        u = u - q[i-t-1] * b**(i-t-1) * v
        ul = [int(x) for x in str(u)]
        
        if u < 0:
            u = u + v * b**(i-t-1)
            ul = [int(x) for x in str(u)]
            
            q[i-t-1] -= 1
        
        i -= 1
    
    return int(''.join(str(x) for x in q)), u
```
Результатом запуска функции будет рис. [-@fig:alg5res].

![Проверка функции](image/alg5res.png){ #fig:alg5res width=100% }

Можно видеть, что был получен верный результат для каждого алгоритма, и функции работают корректно.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с целочисленной арифметикой многократной точности.
Также была получена реализация на языке Python алгоритмов сложения неотрицательных целых чисел, вычитания неотрицательных целых чисел, 
умножения неотрицательных целых чисел, быстрый столбик и деления многоразрядных целых чисел.

# Список литературы{.unnumbered}

::: {#refs}
:::
