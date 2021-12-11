---
# Front matter
title: "Отчёт по лабораторной работе №5"
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
Цель: Ознакомиться с некоторыми вероятностными алгоритмами проверки чисел на простоту.

# Задание
Программно реализовать следующие вероятностные алгоритмы проверки чисел на простоту: тест Ферма, тест Соловэя-Штрассена, тест Миллера-Рабина. А также алгоритм вычисления символа Якоби.

# Теоретическое введение
Нахождение алгоритма, который правильно и эффективно проверяет очень большое целое число и устанавливает: данное число – простое или же составное, — всегда было проблемой в теории чисел и, следовательно, в криптографии.
Алгоритмы, которые решают эту проблему, могут быть разделены на две обширные категории — детерминированные и вероятностные.
Детерминированный алгоритм всегда даёт точный ответ.
А вероятностные тесты в большинстве своём однозначно определяют, если число составное, но не обеспечивают математического доказательства простоты, когда оно определяется вероятно простым.
Не смотря на это, детерминированные алгоритмы обычно менее эффективны, чем вероятностные.
Это обусловлено тем, что детерминированные, как правило, требуют больших вычислительных мощностей, и в то же время для вероятностных можно получить вероятность ошибки настолько маленькую,
что это почти гарантирует, что алгоритм вырабатывает правильный ответ [@intuit;@cryptowiki].

Первый вероятностный метод, который мы рассмотрим, — испытание простоты чисел тестом Ферма. В основе теста лежит малая теорема Ферма:

$a^{n-1} \equiv 1 (\mod n).$

Если $n$ – целое число, чья простота под вопросом, нахождение такого $a$ в интервале $1 \leq a \leq n-1$, что это равенство не выполняется, докажет, что $n$ – составное. 
И наоборот, если найти целое число $a$, что равенство выполняется, утверждается, что $n$ – простое, в том смысле, что оно удовлетворяет теореме Ферма для основания $a$. 
Отсюда вытекает следующее определение. Составное n такое, что равенство выполняется, называется псевдопростым по основанию $a$ [@intuit;@cryptowiki].

Другой тест - тест Соловэя-Штрассена использует  критерий Эйлера для определения значения символа Лежандра (квадратичного характера числа по простому модулю).
В самом тесте, естественно, вычисляется символ Якоби по модулю $n$.
Нечётное целое число n является простым тогда и только тогда, когда для всех чисел $a: 1 \leq a \leq n-1$ выполняется сравнение вида:

$a^{(n-1)/2} \equiv \left( \frac{a}{n} \right) (\mod n)$.

Если $n$ простое, то данное сравнение, очевидно, выполнено в силу свойств символа Лежандра [@studfiles].

Рассмотрим ещё один метод – тест Миллера-Рабина. Пусть $n$ – нечётное число большее 1. Число $n - 1$ однозначно представляется в виде $n - 1 = 2^st$, где $s$ – целое, $t$ – нечётное.
Целое число $a \in (1; n)$, называется свидетелем простоты числа $n$, если выполняется одно из условий:

$a^t \equiv 1 (\mod n),$

или существует целое число $k: 0 \leq k < s$, такое, что

$a^{2^kt} \equiv n - 1 (\mod n).$

Таким образом, для данного $n$ находятся подходящие $s$ и $t$, выбирается случайное число $a \in (1; n)$.
Если $a \in (1; n)$ не является свидетелем простоты числа $n$, то выдается ответ «составное», и алгоритм завершается. 
Иначе, выбирается новое случайное число $a$, и процедура проверки повторяется.
После нахождения заданного числа свидетелей простоты выдаётся ответ «вероятно простое», и алгоритм завершается.
Данный алгоритм интересен также тем, что для $r$ прошедших проверку $a$, вероятность того, что кандидат окажется составным не превосходит $4^{-r}$ [@cryptowiki].


# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбран язык Python. Далее реализуем представленные алгоритмы в виде функций в соответствии псевдокоду из задания к лабораторной работе. Перед началом работы подключим библиотеку numpy:
```
import numpy as np
```

Сначала реализуем тест Ферма:
```
# n - нечётное целое число >= 5

def Fermat(n):
    a = np.random.randint(2, n-1)
    r = a**(n-1) % n
    if r == 1:
        return 'Число n, вероятно, простое'
    else:
        return 'Число n составное'
```
Результатом запуска функции будет рис. [-@fig:Fermat].

![Проверка функции теста Ферма](image/Fermat.png){ #fig:Fermat width=100% }

Так как для теста Соловэя-Штрассена необходимо вычисление символа Якоби, реализуем алгоритм его вычисления:
```
# n - нечётное целое число >= 3
# a - целое число 0<=a<n

def Jacobi(a, n):
    g = 1
    while True:
        if a == 0:
            return 0
        if a == 1:
            return g

        k = 0
        a1 = a
        while a1 % 2 == 0:
            a1 = int(a1 / 2)
            k += 1
        
        if k % 2 == 0:
            s = 1
        else:
            if (n-1) % 8 == 0 or (n+1) % 8 == 0:
                s = 1
            if (n-3) % 8 == 0 or (n+3) % 8 == 0:
                s = -1

        if a1 == 1:
            return g*s

        if (n-3) % 4 == 0 and (a1-3) % 4 == 0:
            s = -s

        a = n % a1
        n = a1
        g = g*s
```
Результатом запуска функции будет рис. [-@fig:Jacobi].

![Проверка функции вычисления символа Якоби](image/Jacobi.png){ #fig:Jacobi width=100% }

Теперь реализуем тест Соловэя-Штрассена:
```
# n - нечётное целое число >= 5

def SolStr(n):
    a = np.random.randint(2, n-2)
    r = a**int((n-1)/2) % n

    if r != 1 and r != n-1:
        return 'Число n составное'
    
    s = Jacobi(a, n)
    
    if r != s % n:
        return 'Число n составное'
    else:
        return 'Число n, вероятно, простое'
```
Результатом запуска функции будет рис. [-@fig:SolStr].

![Проверка функции теста Соловэя-Штрассена](image/SolStr.png){ #fig:SolStr width=100% }

Наконец, реализуем последний алгоритм - тест Миллера-Рабина:
```
# n - нечётное целое число >= 5

def MillRab(n):
    s = 0
    r = n - 1
    while r % 2 == 0:
        r = int(r / 2)
        s += 1

    a = np.random.randint(2, n-2)
    
    y = a**r % n

    if y != 1 and y != n-1:
        j = 1
        while j <= s-1 and y != n-1:
            y = y**2 % n
            if y == 1:
                return 'Число n составное'
            j += 1
        if y != n-1:
            return 'Число n составное'
    
    return 'Число n, вероятно, простое'
```
Результатом запуска функции будет рис. [-@fig:MillRab].

![Проверка функции теста Миллера-Рабина](image/MillRab.png){ #fig:MillRab width=100% }

Можно видеть, что все функции тестов дали одинаковый верны результат, и функция вычисления символа Якоби также работает корректно.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с некоторыми вероятностными алгоритмами проверки чисел на простоту: тест Ферма, тест Соловэя-Штрассена и тест Миллера-Рабина.
Также была получена реализация на языке Python рассмотренных алгоритмов, а также алгоритма вычисления символа Якоби.

# Список литературы{.unnumbered}

::: {#refs}
:::
