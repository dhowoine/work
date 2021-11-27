---
# Front matter
title: "Отчёт по лабораторной работе №3"
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
Цель: Ознакомиться с шифрованием гаммированием.

# Задание
Программно реализовать алгоритм шифрование гаммированием конечной гаммой.

# Теоретическое введение
Гаммирование, или Шифр XOR, — метод симметричного шифрования, заключающийся в «наложении» последовательности, состоящей из случайных чисел, на открытый текст.
Последовательность случайных чисел называется гамма-последовательностью и используется для зашифровывания и расшифровывания данных [@wiki].
Шифрование выполняется путем сложения символов исходного текста и ключа по модулю, равному числу букв в алфавите. Если в исходном алфавите, например, 33 символа, то сложение производится по модулю 33.
Такой процесс сложения исходного текста и ключа называется в криптографии наложением гаммы.
Если гамма короче, чем сообщение, предназначенное для зашифрования, гамма повторяется требуемое число раз.
Пусть символам исходного алфавита соответствуют числа от 0 (А) до 32 (Я). Можно записать правило гаммирования следующим образом:

$z = x + k (mod N)$,

где $x$ - исходный символ, $k$ - символ гаммы,  $z$ – закодированный символ, $N$ - количество символов в алфавите, а сложение по модулю $N$ - операция, аналогичная обычному сложению, с тем отличием, что если обычное суммирование дает результат, больший или равный $N$,
то значением суммы считается остаток от деления его на $N$ [@intuit].

Различают гаммирование с конечной и бесконечной гаммами. В качестве конечной гаммы может
использоваться фраза, в качестве бесконечной - последовательность, вырабатываемая генератором псевдослучайных чисел [@book].
Наиболее часто на практике встречается двоичное гаммирование. При этом используется двоичный алфавит, а сложение производится по модулю два [@intuit].
В том случае, если множеством используемых для шифрования
знаков сообщения является текст, отличный от двоичного кода, то
его символы и символы гаммы заменяются цифровыми
эквивалентами, которые затем суммируются по модулю $N$ [@book].
Eсли ключ является фрагментом истинно
случайной последовательности с равномерным законом
распределения, причем его длина равна длине исходного
сообщения и используется этот ключ только один раз, после чего
уничтожается, такой шифр является абсолютно стойким, его
невозможно раскрыть, даже если криптоаналитик располагает
неограниченным запасом времени и неограниченным набором
вычислительных ресурсов [@book].

Операция сложения по модулю 2 часто обозначается $\oplus$, то есть можно записать:

$z = x \oplus k$.

Таким образом, при гаммировании по модулю 2 нужно использовать одну и ту же операцию как для зашифрования, так и для расшифрования.
Это позволяет использовать один и тот же алгоритм, а соответственно и одну и ту же программу при программной реализации, как для шифрования, так и для расшифрования [@intuit]. 

# Выполнение лабораторной работы
Для выполнения лабораторной работы был выбрат язык Python. Перед началом работы подключим библиотеку numpy:
```
import numpy as np
```

Реализуем шифрование гаммированием конечной гаммой в виде функции:
```
# C - открытый текст
# g - гамма

def gamm(C, g):
    C = C.replace(' ', '')
    for i in range(int(np.floor(len(C)/len(g) - 1))):
        g += ''.join(g)
    
    g += ''.join(g[:len(C)%len(g)])
    
    if ord('a') <= ord(C[0]) <= ord('z'):
        n = 26
        s = ord('a')
        
    if ord('а') <= ord(C[0]) <= ord('я'):
        n = 33
        s = ord('а')
        
    cypher = ''
    
    for i in range(len(C)):
        c = (ord(C[i]) + ord(g[i]) - 2*s) % n + 1
        cypher += ''.join(chr(c + s))
        
    return cypher
```
Результатом запуска функции для примера из задания к лабораторной работе будет рис. [-@fig:gammaRU].

![Проверка функции 1](image/gammaRU.png){ #fig:gammaRU width=100% }

Можно видеть, что полученное зашифрованное сообщение совпадает с приведённым в задании к лабораторной.
Таким образом, шифрование функцией было произведено корректно.

Также проверим работу функции для отрытого текста и гаммы на английском языке (рис. [-@fig:gammaEN]).

![Проверка функции 2](image/gammaEN.png){ #fig:gammaEN width=100% }

Видим, что функция отработала нормально и для второго возможного алфавита.

# Выводы
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.
Было осуществлено знакомство с новым методом шифрования - шифрованием гаммированием.
Также была получена реализация алгоритма шифрования гаммированием конечной гаммой для русского и английского алфавита нижних регистров на языке Python.

# Список литературы{.unnumbered}

::: {#refs}
:::
