---
## Front matter
lang: ru-RU
title: |
    Отчёт по лабораторной работе №5.  
    Вероятностные алгоритмы проверки чисел на простоту
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

Цель: Ознакомиться с некоторыми вероятностными алгоритмами проверки чисел на простоту.

Задача: Программно реализовать следующие вероятностные алгоритмы проверки чисел на простоту: тест Ферма, тест Соловэя-Штрассена, тест Миллера-Рабина. А также алгоритм вычисления символа Якоби.

## Теоретическое введение
Тесты на простоту: детерминированные и вероятностные.

- *Детерминированные тесты* - однозначно определяют простое число, или нет; требуют больших вычислительных мощностей.

- *Вероятностные тесты* - делают более слабое утверждение; определяют, число вероятно простое, или составное.


## тест Ферма
Для простого числа $n$ и $a: 1 \leq a \leq n-1$ выполняется равенство:

$a^{n-1} \equiv 1 (\mod n).$

Проверка функции теста Ферма:
![Проверка функции теста Ферма](image/Fermat.png){ #fig:Fermat width=100% }


## алгоритм вычисления символа Якоби
Символ Якоби $\left( \frac{m}{n} \right) = \left( \frac{m}{p_1} \right) ... \left( \frac{m}{p_r} \right)$, где
$m, n \in Z, n = p_1...p_r, p_i \ne 2$ - простые (не обязательно различные)

Проверка функции вычисления символа Якоби:
![Проверка функции вычисления символа Якоби](image/Jacobi.png){ #fig:Jacobi width=100% }


## тест Соловэя-Штрассена
Для простого числа $n$ и $a: 1 \leq a \leq n-1$ выполняется равенство:

$a^{(n-1)/2} \equiv \left( \frac{a}{n} \right) (\mod n)$.

Проверка функции теста Соловэя-Штрассена:
![Проверка функции теста Соловэя-Штрассена](image/SolStr.png){ #fig:SolStr width=100% }


## тест Миллера-Рабина
Для простого числа $n$, причём $n - 1 = 2^st$, где $s$ – целое, $t$ – нечётное, и $a: 1 \leq a \leq n-1$ выполняется хотя бы одно из условий:

- $a^t \equiv 1 (\mod n)$

- $a^{2^kt} \equiv n - 1 (\mod n), k: 0 \leq k < s$

Проверка функции теста Миллера-Рабина:
![Проверка функции теста Миллера-Рабина](image/MillRab.png){ #fig:MillRab width=100% }


## Заключение
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.

- Было осуществлено знакомство с некоторыми вероятностными алгоритмами проверки чисел на простоту: тест Ферма, тест Соловэя-Штрассена и тест Миллера-Рабина.

- Также была получена реализация на языке Python рассмотренных алгоритмов, а также алгоритма вычисления символа Якоби.



# Спасибо за внимание
