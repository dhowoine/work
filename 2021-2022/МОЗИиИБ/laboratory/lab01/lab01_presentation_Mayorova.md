---
## Front matter
lang: ru-RU
title: |
    Отчёт по лабораторной работе №1.  
    Шифры простой замены
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

Цель: Ознакомиться с шифрами простой замены на примере шифров Цезаря и Атбаш.

Задачи: 

- Рассмотреть и реализовать шифр Цезаря с произвольным ключом *k*.
- Рассмотреть и реализовать шифр Атбаш.

## Теоретическое введение
**Шифр простой замены** - шифрование, осуществляемое путём создания  таблицы шифрования,
в которой каждой букве открытого текста сопоставляется по определённому алгоритму единственная буква шифр-текста.

**Шифр Цезаря**: шифроалфавит представляет собой сдвинутый исходный алфавит на *k* позиций.

**Шифр Атбаш**: шифроалфавит представляет собой отражённый исходный алфавит. 

## Реализация шифра Цезаря
Функция на языке Python:
```
# c - буква для шифрования
# k - ключ

def Caesar(с, k):
    n = [(i + k) % 26 for i in range(26)][ord(c) - ord('a')]
    return chr(ord('a') + n)
```

## Проверка реализации шифра Цезаря
- для ключа *k*=3: "Veni vidi vici" -> YHQL YLGL YLFL
![Проверка шифра Цезаря 1](image/Caesar1.png){ #fig:Caesar1 width=100% }

- для ключа *k*=1: "Festina lente" -> GFTUJOB MFOUF
![Проверка шифра Цезаря 2](image/Caesar2.png){ #fig:Caesar2 width=100% }

## Реализация и проверка реализации шифра Атбаш
Функция на языке Python:
```
# c - буква для шифрования
def Atbash(c):
    return chr(ord('а') + (ord('я') - ord(c)))
```

Проверка 1:
![Проверка шифра Атбаш 1](image/Atbash1.png){ #fig:Atbash1 width=80% }

Проверка 2:
![Проверка шифра Атбаш 2](image/Atbash2.png){ #fig:Atbash2 width=80% }

## Заключение
Таким образом, была достигнута цель, поставленная в начале лабораторной работы.

- Было осуществлено знакомство с шифрами простой замены на примере шифров Цезаря и Атбаш.
- Была получена реализация шифра Цезаря с произвольным ключом *k* для латинского алфавита нижнего регистра.
- Была получена реализация шифра Атбаш для кириллицы нижнего регистра.

# Спасибо за внимание
