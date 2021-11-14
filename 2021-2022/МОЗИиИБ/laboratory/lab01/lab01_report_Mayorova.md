---
# Front matter
title: "Отчёт по лабораторной работе №1"
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

Цель: Ознакомиться с шифрами простой замены на примере шифров Цезаря и Атбаш.

# Задание

1. Реализовать шифр Цезаря с произвольным ключом *k*.
2. Реализовать шифр Атбаш.

# Теоретическое введение

Шифр простой замены — класс методов шифрования, которые сводятся к созданию по определённому алгоритму таблицы шифрования,
в которой для каждой буквы открытого текста существует единственная сопоставленная ей буква шифр-текста. Само шифрование заключается в замене букв согласно таблице.
Для расшифровки достаточно иметь ту же таблицу, либо знать алгоритм, по которому она генерируется.
К шифрам простой замены относятся многие способы шифрования, возникшие в древности или средневековье, как, например, Атбаш или шифр Цезаря [@cypher].

Шифр Цезаря — один из древнейших шифров. При шифровании каждый символ в открытом тексте заменяется другим, отстоящим левее или правее от него в алфавите на фиксированное число позиций.
Шифр назван в честь римского полководца Гая Юлия Цезаря, использовавшего его для секретной переписки со своими генералами. Например, Цезарь использовал в переписке шифр с ключом *k*=3.
Такая таблица шифрования имеет вид табл. [-@tbl:Caesar1].

: Шифр Цезаря, используемый Цезарем {#tbl:Caesar1}

| A | B | C | D | E | F | G | H | I | J | ... | Q | R | S | T | U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|-----|---|---|---|---|---|---|---|---|---|---|
| D | E | F | G | H | I | J | K | L | M | ... | T | U | V | W | X | Y | Z | A | B | C |

Если сопоставить каждому символу алфавита его порядковый номер (нумеруя с 0), то шифрование и дешифрование можно выразить формулами:

*y* = (*x - k*) mod *n*

*x* = (*y - k*) mod *n*,
 
где

- *x* — символ открытого текста
- *y* — символ шифрованного текста
- *n* — мощность (кол-во символов) алфавита
- *k* — ключ.

С точки зрения современного криптоанализа, шифр Цезаря не имеет приемлемой стойкости [@CaesarW;@Caesar2].

Шифр Атбаш — простой шифр подстановки для алфавитного письма, использованный для еврейского алфавита и получивший оттуда свое название.
Шифрование происходит заменой первой буквы алфавита на последнюю, второй на предпоследнюю, то есть правило шифрования состоит в замене *i*-й буквы алфавита буквой с номером *n*-*i*+1, где *n* — число букв в алфавите [@AtbashW;@Atbash2].
Для кириллицы таблица шифрования будет иметь вид табл. [-@tbl:Atbash].

: Шифр Атбаш для кириллицы {#tbl:Atbash}

| а | б | в | г | д | е | ё | ж | з | и | ... | ц | ч | ш | щ | ъ | ы | ь | э | ю | я |
|---|---|---|---|---|---|---|---|---|---|-----|---|---|---|---|---|---|---|---|---|---|
| я | ю | э | ь | ы | ъ | щ | ш | ч | ц | ... | и | з | ж | ё | е | д | г | в | б | а |

# Выполнение лабораторной работы

Для выполнения лабораторной работы был выбрат язык Python. Сначала реализуем шифр Цезаря с произвольным ключом *k* для латинского алфавита нижнего регистра.

```
# c - буква для шифрования
# k - ключ

def Caesar(с, k):
    n = [(i + k) % 26 for i in range(26)][ord(c) - ord('a')]
    return chr(ord('a') + n)
```

Проверим работу функции на примере донесения Ю. Цезаря Сенату об одержанной им победе над Понтийским царем: YHQL YLGL YLFL ("Veni, vidi, vici" - лат. "Пришёл, увидел, победил")
для ключа *k*=3 (табл. [-@tbl:Caesar1]).

![Проверка шифра Цезаря 1](image/Caesar1.png){ #fig:Caesar1 width=100% }

В результате видим, что сообщение было зашифровано корректно (рис. [-@fig:Caesar1]).

Ещё раз проверим работу функции уже на любимом изречении императора Августа, который использовал шифр Цезаря с ключом *k*=1 (табл. [-@tbl:Caesar2]):
GFTUJOB MFOUF ("Festina lente" - лат. "Торопись медленно").

: Шифр Цезаря, используемый Августом {#tbl:Caesar2}

| A | B | C | D | E | F | G | H | I | J | ... | Q | R | S | T | U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|-----|---|---|---|---|---|---|---|---|---|---|
| B | C | D | E | F | G | H | I | J | K | ... | R | S | T | U | V | W | X | Y | Z | A |


![Проверка шифра Цезаря 2](image/Caesar2.png){ #fig:Caesar2 width=100% }

В результате видим, что изречение было зашифровано корректно (рис. [-@fig:Caesar2]).

Далее реализуем шифр Атбаш для кириллицы нижнего регистра (табл. [-@tbl:Atbash]).

```
# c - буква для шифрования

def Atbash(c):
    return chr(ord('а') + (ord('я') - ord(c)))
```

Проверим работу функции для первой и последней букв алфавита (рис. [-@fig:Atbash1]) и для аббревиатуры нашей изучаемой дисциплины (рис. [-@fig:Atbash2]).

![Проверка шифра Атбаш 1](image/Atbash1.png){ #fig:Atbash1 width=100% }

![Проверка шифра Атбаш 2](image/Atbash2.png){ #fig:Atbash2 width=100% }

Можно видеть, что шифрование функцией было произведено корректно.

# Выводы

Таким образом, была достигнута цель, поставленная в начале лабораторной работы. Было осуществлено знакомство с шифрами простой замены на примере
шифров Цезаря и Атбаш. Также была получена реализация данных шифров на языке Python.

# Список литературы{.unnumbered}

::: {#refs}
:::
