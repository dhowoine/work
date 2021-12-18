---
## Front matter
lang: ru-RU
title: |
    Отчёт по лабораторной работе №6.  
    Разложение чисел на множители
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

Цель: Ознакомиться с задачей разложения составного числа на множители.

Задача: Программно реализовать $\rho$-метод Полларда.

## Теоретическое введение
*Факторизация* — разложение натурального числа в произведение простых множителей.

*Основная теорема арифметики*: $n  = p^{e1}_1 \times p_{2}^{e_2} \times \dots \times p_{k}^{e_k}$, где $p_1, p_2,..., p_k$ — простые числа и $e_1, e_2,..., e_k$ — положительные целые числа.

## $\rho$-метод Полларда
_Вход_: Число $n$, начально значение $c$, функция $f$, обладающая сжимающими свойствами.

1. Положить $a \leftarrow c, b \leftarrow c$

2. Вычислить $a \leftarrow f(a)(\mod n), b \leftarrow f(f(b))(\mod n)$

3. Найти $d \leftarrow$ НОД$(a - b, n)$

4. Если $1 < d < n$, то результат $d$. При $d = n$ результат "Делитель не найден". При $d = 1$ вернуться на шаг 2.


## Реализация $\rho$-метода Полларда
Положительное целое число $n = 1359331$

Начальное значение $c = 1$

Функция, обладающая сжимающими свойствами: $f(x) = (x^2 + 5) \mod n$

Проверка функции $\rho$-метода Полларда:
![Проверка функции](image/Pollard.png){ #fig:Pollard width=100% }


## Заключение
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.

- Было осуществлено знакомство с задачей разложения составного числа на два нетривиальных сомножителя.

- Также была получена реализация на языке Python $\rho$-метода Полларда.



# Спасибо за внимание
