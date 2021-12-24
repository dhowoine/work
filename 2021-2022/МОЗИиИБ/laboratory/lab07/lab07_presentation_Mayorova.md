---
## Front matter
lang: ru-RU
title: |
    Отчёт по лабораторной работе №7.  
    Дискретное логарифмирование в конечном поле
author: |
    *Дисциплина: Математические основы защиты информации*  
    *и информационной безопасности*  
    \vspace{2pt}  
    **Студент:** Майорова О.А., 1032212322  
		**Группа:** НФИмд-02-21  
		**Преподаватель:** д.ф.-м.н., Кулябов Д. С. 
    \vspace{2pt}
date: Москва, 2021

## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
linestretch: 1.25

mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.7
---

## Цель и задачи

Цель: Ознакомиться с задачей дискретного логарифмирования в конечном поле.

Задача: Программно реализовать $\rho$-метод Полларда для задач дискретного логарифмирования.


## $\rho$-метод Полларда
_Вход_: Простое число $p$, число $a$ порядка $r$ по модулю $p$, целое число $b: 1 < b < p$, $f$ - отображение, обл-ее сжимающими св-ми и сохраняющее вычислимость логарифма.

1. Выбрать произвольные целые числа $u, v$ и положить $c \leftarrow a^ub^v (\mod p)$, $d \leftarrow c$.

2. Выполнять $c \leftarrow f(c)(\mod p), d \leftarrow f(f(d))(\mod p)$, вычисляя при этом логарифмы для $c$ и $d$ как линейные функции от $x$ по модулю $r$, до получения равенства $c \equiv d (\mod p)$.

3. Приравняв логарифмы для $c$ и $d$, вычислить логарифм $x$ решением сравнения по модулю $r$. Результат: $x$ или "Решений нет".


## Реализация $\rho$-метода Полларда
Задача: $10^x \equiv 64 (\mod 107)$

Пусть $u = 2, v = 2$

Отображение: $f(c) = \begin{cases} 10c (\mod 107) & c < 53 \\ 64c (\mod 107) & c \ge 53 \end{cases}$

Проверка функции $\rho$-метода Полларда для задач дискретного логарифмирования:
![Проверка функции](image/PollardLog.png){ #fig:PollardLog width=100% }


## Заключение
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.

- Было осуществлено знакомство с задачей дискретного логарифмирования в конечном поле.

- Также была получена реализация на языке Python $\rho$-метода Полларда для задач дискретного логарифмирования.



# Спасибо за внимание
