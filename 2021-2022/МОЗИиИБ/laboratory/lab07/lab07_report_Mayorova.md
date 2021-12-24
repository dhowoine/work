---
# Front matter
title: "Отчёт по лабораторной работе №7"
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
Цель: Ознакомиться с задачей дискретного логарифмирования в конечном поле.


# Задание
Программно реализовать $\rho$-метод Полларда для задач дискретного логарифмирования.

# Теоретическое введение
Дискретное логарифмирование (DLOG) — задача обращения функции $g^{x}$ в некоторой конечной мультипликативной группе $G$.
Наиболее часто задачу дискретного логарифмирования рассматривают в мультипликативной группе кольца вычетов или конечного поля, а также в группе точек эллиптической кривой над конечным полем.
Эффективные алгоритмы для решения задачи дискретного логарифмирования в общем случае неизвестны.
Для заданных $g$ и $a$ решение x уравнения $g^{x}=a$ называется дискретным логарифмом элемента $a$ по основанию $g$.
В случае, когда $G$ является мультипликативной группой кольца вычетов по модулю $m$, решение называют также индексом числа $a$ по основанию $g$.
Индекс числа $a$ по основанию $g$ гарантированно существует, если $g$ является первообразным корнем по модулю $m$.
Решение задачи дискретного логарифмирования состоит в нахождении некоторого целого неотрицательного числа $x$, удовлетворяющего уравнению $g^{x}=a$.
Если оно разрешимо, у него должно быть хотя бы одно натуральное решение, не превышающее порядок группы.
Это сразу даёт грубую оценку сложности алгоритма поиска решений сверху — алгоритм полного перебора нашёл бы решение за число шагов не выше порядка данной группы.
В кольце вычетов по простому модулю одним из алгоритмов решения задачи с экспоненциальной сложностью является $\rho$-метод Полларда [@wiki].

На вход алгоритму подаются ростое число $p$, число $a$ порядка $r$ по модулю $p$, целое число $b: 1 < b < p$ и $f$ - отображение, обл-ее сжимающими св-ми и сохраняющее вычислимость логарифма.
Для дискретного логарифмирования в качестве случайного отображения $f$ чаще всего используются ветвящиеся отображения, например:

$f(c) = \begin{cases} ac & c < p/2 \\ bc & c > p/2 \end{cases}$

При $c < p/2$ имеем $\log _{a} f(c) = \log _{a} c + 1$, при $c > p/2$ имеем $\log _{a} f(c) = \log _{a} c + x$.

1. Выбрать произвольные целые числа $u, v$ и положить $c \leftarrow a^ub^v (\mod p), d \leftarrow c$.

2. Выполнять $c \leftarrow f(c)(\mod p), d \leftarrow f(f(d))(\mod p)$, вычисляя при этом логарифмы для $c$ и $d$ как линейные функции от $x$ по модулю $r$, до получения равенства $c \equiv d (\mod p)$.

3. Приравняв логарифмы для $c$ и $d$, вычислить логарифм $x$ решением сравнения по модулю $r$. Результат: $x$ или "Решений нет".

Задача дискретного логарифмирования, как и задача разложения на множители, применяется во многих алгоритмах криптографии с открытым ключом.
Предложенная в 1976 году У. Диффи и М. Хеллманом для установления сеансового ключа, эта задача послужила основой для создания протоколов
шифрования и цифровой подписи, доказательств с нулевым разглашением и других криптографических протоколов [@lab].

# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбран язык Python. Далее реализуем представленный алгоритм в виде функции в соответствии с описанием из задания к лабораторной работе.

Сначала реализуем функцию вычисления ветвящегося отображения и этом логарифмов для $c$ и $d$:
```
def f(c, u, v):
    if c < 53:
        return 10*c % 107, u+1, v
    else:
        return 64*c % 107, u, v+1
```

Также, для вычисления наибольшего общего делителя, используем функцию, реализующую расширенный алгоритм Евклида, из лабораторной работы 4:
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

Наконец, реализуем $\rho$-метод Полларда для задач дискретного логарифмирования:
```
def PollardLog(p, a, r, b, u, v):
    c = a**u * b**v % p
    d = c
    uc, vc = u, v
    ud, vd = u, v
    
    c, uc, vc = f(c, uc, vc)
    c %= p
    d, ud, vd = f(*f(d, ud, vd))
    d %= p
    
    while c%p != d%p:
        c, uc, vc = f(c, uc, vc)
        c %= p
        d, ud, vd = f(*f(d, ud, vd))
        d %= p

    v = vc - vd
    u = ud - uc
    
    d, x, y = ExtEuclid(v, r)
    
    while d != 1:
        v /= d
        u /= d
        r /= d
        d, x, y = ExtEuclid(v, r)
    
    return x*u % r
```
Результатом запуска функции будет рис. [-@fig:PollardLog].

![Проверка функции](image/PollardLog.png){ #fig:PollardLog width=100% }

Можно видеть, что был получен верный результат, и функция работает корректно.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с задачей дискретного логарифмирования в конечном поле.
Также была получена реализация на языке Python $\rho$-метода Полларда для задач дискретного логарифмирования.

# Список литературы{.unnumbered}

::: {#refs}
:::
