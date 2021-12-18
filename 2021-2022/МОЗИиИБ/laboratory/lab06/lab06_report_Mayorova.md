---
# Front matter
title: "Отчёт по лабораторной работе №6"
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
Цель: Ознакомиться с задачей разложения составного числа на множители.

# Задание
Программно реализовать $\rho$-метод Полларда.

# Теоретическое введение
Факторизацией натурального числа называется его разложение в произведение простых множителей.
Существование и единственность (с точностью до порядка следования множителей) такого разложения следует из основной теоремы арифметики [@wiki].
Согласно основной теореме арифметики любое положительное целое число больше единицы может быть уникально записано в
следующей главной форме разложения на множители, где $p_1, p_2,..., p_k$ — простые числа и $e_1, e_2,..., e_k$ — положительные целые числа:

$n  = p^{e1}_1 \times p_{2}^{e_2} \times \dots \times p_{k}^{e_k}.$

Есть непосредственные приложения разложения на множители, такие как вычисление наибольшего общего делителя и наименьшего общего множителя [@intuit].
Предположение о том, что для больших чисел задача факторизации является вычислительно сложной, лежит в основе широко используемых алгоритмов (например, RSA).
Задача поиска эффективных способов разложения целых чисел на множители интересовала математиков с давних времён, особенно специалистов в области теории чисел. 
Как правило, на вход таких алгоритмов подаётся число $n \in N$, которое необходимо факторизовать, состоящее из $N = ( \log_2 n ) + 1$ символов, если $n$ представлено в двоичном виде [@wiki].

В 1975 г. Джон М. Поллард разработал метод для разложения на множители, который базируется на следующих положениях:

1. Предположим, что есть два целых числа, $x_1$ и $x_2$, таких, что $p$ делит $x_1 – x_2$, но эта разность не делится на $n$.

2. Может быть доказано, что $p =$ НОД$(x_1 – x_2, n)$. Поскольку $p$ делит $x_1 – x_2$, можно записать, что $x_1 – x_2 = q \times p$. Но поскольку $n$ не делит $x_1 – x_2$, очевидно, что $q$ не делится на $n$. Это означает, что НОД$(x_1 – x_2, n)$ является либо 1, либо сомножителем.

Следующий алгоритм повторно выбирает $x_1$ и $x_2$, пока не находит соответствующую пару:

1. Выберите $x_1$ — малое случайное целое число, называемое первоисточником.

2. Используйте функцию, чтобы вычислить $x_2$, такую, чтобы $n$ не делило $x_1 – x_2$. Функция, которая может быть применена, — это $x_2 = f(x_1) = x_{1}^{2} + a$ ($a$ обычно выбирается как 1).

3. Вычислить НОД$(x_1 – x_2, n)$. Если это не 1, результат – сомножитель. Алгоритм останавливается.  Если это 1, то происходит возвращение, чтобы повторить процесс с $x_1$. Теперь мы вычисляем $x_3$. Заметим, что в следующем раунде мы начинаем с $x_3$ и так далее. Если мы перечислим значения нескольких $x$, используя $\rho$-алгоритм Полларда, мы увидим, что дуга значений в конечном счете повторяется, создавая форму, подобную греческой букве $\rho$.

Чтобы уменьшить число итераций, алгоритм был немного изменен. Он начинается с пары $(x_0, x_0)$, и итеративно вычисляет $(x_1, x_2), (x_2, x_4), (x_3, x_6),..., (x_i, x_{2i})$, используя равенство $x_{i+1} = f(x_i)$.
В каждой итерации мы применяем функцию $f(x_i)$ (начиная с шага 2). При этом вычисление идут следующим образом: в паре вычисляется один раз первый элемент и дважды вычисляется второй элемент [@intuit].



# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбран язык Python. Далее реализуем представленный алгоритм в виде функции в соответствии псевдокоду из задания к лабораторной работе.

Сначала реализуем функцию, обладающую сжимающими свойствами:
```
def f(x, n):
    return (x**2 + 5) % n
```

Так как для $\rho$-метода Полларда необходимо вычисление наибольшего общего делителя, используем чуть изменённую функцию, реализующую алгоритм Евклида, из лабораторной работы 4:
```
def Euclid(a, b):
    rp = a
    rc = b
    rn = 1
    while rn != 0:
        rn = rp % rc
        d = rc
        rp = rc
        rc = rn
    
    return d
```

Наконец, реализуем $\rho$-метод Полларда:
```
def Pollard(c, n):
    a = c
    b = c
    while True:
        a = f(a, n) % n
        b = f(f(b, n), n) % n
        d = Euclid(a-b, n)
        if 1 < d < n:
            return d

        if d == n:
            return 'Делитель не найден'
```
Результатом запуска функции будет рис. [-@fig:Pollard].

![Проверка функции](image/Pollard.png){ #fig:Pollard width=100% }

Можно видеть, что был получен верный результат, и функция работает корректно.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с задачей разложения составного числа на два нетривиальных сомножителя.
Также была получена реализация на языке Python $\rho$-метода Полларда.

# Список литературы{.unnumbered}

::: {#refs}
:::
