---
# Front matter
title: "Отчёт по лабораторной работе №4"
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
Цель: Ознакомиться с методами вычисления наибольшего общего делителя.

# Задание
Программно реализовать алгоритмы вычисления наибольшего общего делителя для двух чисел: алгоритм Евклида, бинарный алгоритм Евклида, расширенный алгоритм Евклида, расширенный бинарный алгоритм Евклида.

# Теоретическое введение
Делитель натурального числа — это такое натуральное число, которое делит данное число без остатка. Если у натурального числа больше двух делителей, его называют составным.
Общий делитель нескольких целых чисел — это такое число, которое может быть делителем каждого числа из указанного множества.
Любое число можно разделить на 1, -1 и на само себя. Значит у любого набора целых чисел будет как минимум три общих делителя.
Если общий делитель больше 0 — противоположное ему значение со знаком минус также является общим делителем.
Любое число, не равное 0, имеет конечное число делителей.
Наибольший общий делитель существует и однозначно определён, если хотя бы одно из чисел $a$ или $b$ не равно нулю.
Если $b$ — делитель целого числа $a$, которое не равно нулю, то модуль числа $b$ не может быть больше модуля числа $a$.
Наибольшим общим делителем двух чисел $a$ и $b$ называется наибольшее число, на которое $a$ и $b$ делятся без остатка. Для записи может использоваться аббревиатура НОД.
Для двух чисел можно записать вот так: НОД$(a, b)$.
Пример: для чисел 54 и 24 наибольший общий делитель равен 6, у чисел 12 и 8 общим делителем будет 4.
Понятие наибольшего общего делителя естественным образом обобщается на наборы из более чем двух целых чисел [@skysmart;@wiki].

Для вычисления наибольшего общего делителя двух целых чисел применяется способ повторного деления с остатком, называемый алгоритмом Евклида.
Сложность алгоритма Евклида равна $O(log^2a)$. Корректность алгоритма исходит из следующих утверждений:

- Если числа $a$ и $b$ целые, и $a$ делится на $b$, то $b =$ НОД$(a, b)$;
- Для любых целых чисел $a, b, c$ выполняется равенство НОД$(a + cb, b) =$ НОД$(a, b)$.

Таким образом, для любых $a, b > 0$ алгоритм Евклида останавливается и выдаваемое им число $d$ является наибольшим общим делителем чисел $a$ и $b$ [@studfiles].

Бинарный вариант алгоритма Евклида оказывается более быстрым при реализации на компьютере, поскольку использует двоичное представление чисел $a$ и $b$.
Бинарный алгоритм Евклида основан на следующих свойствах наибольшего общего делителя (считаем, что $0 < b \leq a$):

- Если оба числа $a$ и $b$ четные, то НОД$(a, b) = 2$НОД$(\frac{a}{2},\frac{b}{2})$;
- Если число $a$ нечетное, число $b$ четное, то НОД$(a, b) =$ $НОД(a, \frac{b}{2})$;
- Если оба числа $a$ и $b$ нечетные, $a > b$, то НОД$(a, b) =$ НОД$(a - b, b)$;
- Если $a = b$, то НОД$(a, b) = a$.

Сложность этого алгоритма также равна $O(log^2a)$.

Для расширенного алгоритма Евклида пусть $x, y$ - такие целые числа, что $ax + by = d$, тогда:

1. Положить $r_0 \leftarrow a, r_1 \leftarrow b , x_0 \leftarrow 1, x_1 \leftarrow 0, y_0 \leftarrow 0, y_1 \leftarrow 1, i \leftarrow 1$.
2. Разделить с остатком $r_{i - 1}$ на $r_i$: $r_{i - 1} = q_ir_i + r_{i + 1}$.
3. Если $r_{i + 1} = 0$, то положить $d \leftarrow r_i, x \leftarrow x_i , y \leftarrow y_i$. В противном случае положить $x_{i + 1} \leftarrow x_{i - 1} - q_ix_i, y_{i + 1} \leftarrow y_{i - 1} - q_iy_i , i \leftarrow i + 1$ и вернуться на шаг 2.

Результат: $d, x, y$.

Аналогично для расширенного бинарного алгоритма Евклида (рис. [-@fig:AlgExtBiEuclid]).

![Расширенный бинарный алгоритм Евклида](image/AlgExtBiEuclid.png){ #fig:AlgExtBiEuclid width=100% }

Сложность этих алгоритмов также равна $O(log^2a)$ [@studfiles].

# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбран язык Python. Далее реализуем представленные алгоритмы в виде функций в соответствии с псевдокодом из задания к лабораторной работе.

Сначала реализуем алгоритм Евклида:
```
def Euclid(a, b):
    rp = a
    rc = b
    rn = rp % rc
    d = rc
    while rn != 0:
        rn = rp % rc
        d = rc
        rp = rc
        rc = rn
    
    return d
```
Результатом запуска функции будет рис. [-@fig:Euclid].

![Проверка функции алгоритма Евклида](image/Euclid.png){ #fig:Euclid width=100% }

Реализуем бинарный алгоритм Евклида:
```
def BiEuclid(a, b):
    g = 1
    while a % 2 == 0 and b % 2 == 0:
        a /= 2
        b /= 2
        g *= 2
    
    u = a
    v = b
    while u != 0:
        while u % 2 == 0:
            u /= 2
            
        while v % 2 == 0:
            v /= 2
            
        if u >= v:
            u = u - v
        else:
            v = v - u
    
    d = g*v
    
    return d
```
Результатом запуска функции будет рис. [-@fig:BiEuclid].

![Проверка функции бинарного алгоритма Евклида](image/BiEuclid.png){ #fig:BiEuclid width=100% }

Реализуем расширенный алгоритм Евклида:
```
def ExtEuclid(a, b):
    rp = a
    rc = b
    xp, xc = 1, 0
    yp, yc = 0, 1
    rn = rp % rc
    d = rc
    while rn != 0:
        rn = rp % rc
        q = (rp - rn)/rc
        d, x, y = rc, xc, yc
        
        rp = rc
        rc = rn
        
        xc = xp - q*xc
        xp = x
        
        yc = yp - q*yc
        yp = y
        
    return d, x, y
```
Результатом запуска функции будет рис. [-@fig:ExtEuclid].

![Проверка функции расширенного алгоритма Евклида](image/ExtEuclid.png){ #fig:ExtEuclid width=100% }

Реализуем расширенный бинарный алгоритм Евклида в виде функции:
```
def ExtBiEuclid(a, b):
    g = 1
    while a % 2 == 0 and b % 2 == 0:
        a /= 2
        b /= 2
        g *= 2
        
    u, v = a, b
    A, B, C, D = 1, 0, 0, 1
    
    while u != 0:
        while u % 2 == 0:
            u /= 2
            if A % 2 == 0 and B % 2 == 0:
                A /= 2
                B /= 2
            else:
                A = (A + b) / 2
                B = (B - a) / 2
            
        while v % 2 == 0:
            v /= 2
            if C % 2 == 0 and D % 2 == 0:
                C /= 2
                D /= 2
            else:
                C = (C + b) / 2
                D = (D - a) / 2
        
        if u >= v:
            u = u - v
            A = A - C
            B = B - D
        else:
            v = v - u
            C = C - A
            D = D - B
    
    d, x, y = g*v, C, D
    
    return d, x, y
```
Результатом запуска функции будет рис. [-@fig:ExtBiEuclid].

![Проверка функции расширенного бинарного алгоритма Евклида](image/ExtBiEuclid.png){ #fig:ExtBiEuclid width=100% }

Можно видеть, что полученные наибольшие общие делители для двух примеров совпали для всех четырёх функций.
Таким образом, можно сказать, что нахождение НОД функциями было произведено корректно.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с методами вычисления наибольшего общего делителя чисел: алгоритм Евклида, бинарный алгоритм Евклида, расширенный алгоритм Евклида, расширенный бинарный алгоритм Евклида.
Также была получена реализация на языке Python рассмотренных алгоритмов для двух чисел.

# Список литературы{.unnumbered}

::: {#refs}
:::
