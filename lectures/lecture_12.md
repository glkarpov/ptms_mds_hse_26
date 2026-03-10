---
title: "Теория вероятностей и математическая статистика"
subtitle: "Характеристики непрерывных случайных величин."
institute: "ФКН ВШЭ"
author: "Глеб Карпов"
format: 
    beamer:
        pdf-engine: xelatex
        aspectratio: 169
        fontsize: 9pt
        theme: Singapore
        fonmttheme: serif
        section-titles: true
        incremental: false
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---
## Пример: анализ функции плотности

- Пусть функция плотности случайной величины $X$ задана в виде: 

$$
    f_X(x) = 
    \begin{cases}
        0, & x < 0 \\
        cx^2, & 0 \leq x \leq 3 \\
        0, & x > 3
    \end{cases}
$$
Найдите нормировочную константу, построите функцию распределения, посчитайте вероятности $P(-5 < X < 2)$, $P(X > 1)$.

- Проверяем выполнение условия нормировки:
\begin{gather*}
    \int\limits_{-\infty}^{+\infty} f_X(x)dx = 1 \\
    \int\limits_{-\infty}^{0}\textcolor{red}{f_X(x)}dx + \int\limits_{0}^{3}\textcolor{violet}{f_X(x)}dx + \int\limits_{3}^{+\infty} \textcolor{blue}{f_X(x)} dx =
     \int\limits_{-\infty}^{0}\textcolor{red}{0} \, dx + \int\limits_{0}^{3}\textcolor{violet}{cx^2}dx + \int\limits_{3}^{+\infty}\textcolor{blue}{0} \, dx = 1 \\
    c\frac{x^3}{3} \Big|_{0}^{3} = 9c = 1 \longrightarrow c = \frac{1}{9}
\end{gather*}

## Пример: анализ функции плотности
- Используем формальное определение функции распределения: $F_X(x) = P(X \leq x) = \int\limits_{-\infty}^{x}f_X(t)dt$

- Рассматриваем так же три области. Первая область $\forall x < 0$. Мы знаем, что функция плотности в этой области равна нулю.
$$
    \int\limits_{-\infty}^{x}\textcolor{red}{f_X(t)}dt = \int\limits_{-\infty}^{x}\textcolor{red}{0} \, dt = 0
$$

- Вторая область $\forall x \in [0, \, 3]$. Знаем, что на этом интервале у функции плотности определенный вид, плюс не забудем, что мы еще ранее нашли нормировочную константу.
\begin{gather*}
    \int\limits_{-\infty}^{x}f_X(t)dt = \int\limits_{-\infty}^{0}\textcolor{red}{f_X(t)}dt + \int\limits_{0}^{x}\textcolor{violet}{f_X(t)}dt =
    \int\limits_{-\infty}^{0}\textcolor{red}{0} \, dt + \int\limits_{0}^{x}\textcolor{violet}{\frac{1 t^2}{9}}dt = 0+ \frac{t^3}{27} \Big|_{0}^{x} = \frac{x^3}{27}
\end{gather*}

- Третья область $\forall x > 3$:
$$
    \int\limits_{-\infty}^{x}f_X(t)dt = \int\limits_{-\infty}^{0}\textcolor{red}{f_X(t)}dt + \int\limits_{0}^{3}\textcolor{violet}{f_X(t)}dt + \int\limits_{3}^{x} \textcolor{blue}{f_X(t)} dt =
    \int\limits_{-\infty}^{0}\textcolor{red}{0} \, dt + \int\limits_{0}^{3}\textcolor{violet}{\frac{1 t^2}{9}}dt + \int\limits_{3}^{x}\textcolor{blue}{0} \, dt = 1
$$


## Пример: анализ функции плотности

- Финально, корректная запись функции распределения:

\begin{equation*}
    F_X(x) = 
    \begin{cases}
        0, & x < 0 \\
        \frac{x^3}{27}, & 0 \leq x \leq 3 \\
        1, & x > 3
    \end{cases}
\end{equation*}

- Посчитаем вероятности через основное определение и через функцию распределения и сравним результаты.
\begin{align*}
P(-5 < X < 2) & = \int \limits_{-5}^{2} f_X(x) dx = \int\limits_{-5}^{0}\textcolor{red}{f_X(x)}dx + \int\limits_{0}^{2}\textcolor{violet}{f_X(x)}dx = \int\limits_{-5}^{0}\textcolor{red}{0} \, dx + \int\limits_{0}^{2}\textcolor{violet}{\frac{1 x^2}{9}}dx = \frac{x^3}{27} \Big|_{0}^{2} = \frac{8}{27} \\
P(-5 < X < 2) & = F_X(2) - F_X(-5) = \frac{8}{27} - 0\\
P(X > 1) & = \int \limits_{1}^{+\infty} f_X(x) dx = \int\limits_{1}^{3}\textcolor{violet}{f_X(x)}dx + \int\limits_{3}^{+\infty} \textcolor{blue}{f_X(x)} dx =
\int\limits_{1}^{3}\textcolor{violet}{\frac{1 x^2}{9}}dx + \int\limits_{3}^{+\infty}\textcolor{blue}{0} \, dx = \frac{x^3}{27} \Big|_{1}^{3} = \frac{26}{27}\\
P(X > 1) & = F_X(+\infty) - F_X(1) = 1 - \frac{1}{27}
\end{align*}


## Математическое ожидание

\begin{itemize}
    
    \item Напомним, что для дискретной СВ мы вычисляем математическое ожидание как 'взвешенную сумму':
$$
    E[X] = \sum \limits_{i=1}^{n} x_i P(X = x_i), \text { вычисляется для } \forall x_i \in \Omega_X.
$$

    \item Если у нас есть другая СВ $G$, являющаяся функцией от $X$: $G = g(X)$:
$$
    E[g(X)] = \sum \limits_{i=1}^{n} g(x_i) P(X = x_i)
$$

    \item Для непрерывного случая мы заменяем сумму на интеграл:
    \begin{equation*}
        \sum \limits_{i=1}^{n} \colorbox{red!20}{$x_i$} \colorbox{green!20}{$P(X = x_i)$} \Rightarrow \int \limits_{-\infty}^{+\infty} \colorbox{red!20}{$x$} \colorbox{green!20}{$f_X(x) dx$} \qquad
        \sum \limits_{i=1}^{n} \colorbox{red!20}{$g(x_i)$} \colorbox{green!20}{$P(X = x_i)$} \Rightarrow \int \limits_{-\infty}^{+\infty} \colorbox{red!20}{$g(x)$} \colorbox{green!20}{$f_X(x) dx$}
    \end{equation*}

    \item Финально:
    \begin{equation*}
    \boxed{E[X] = \int \limits_{-\infty}^{+\infty} x f_X(x) dx} \qquad
    \boxed{E[g(X)] = \int \limits_{-\infty}^{+\infty} g(x) f_X(x) dx}
    \end{equation*}
\end{itemize}

## Дисперсия

\begin{itemize}
    \item Формула для дисперсии остается той же:
$$
    Var[X] = E \left[ (X - E[X])^2 \right] = E[X^2] - (E[X])^2
$$

    \item Напомним доказательство:
\begin{multline*}
    Var[X] = E \left[ (X - E[X])^2 \right] = E[X^2 - 2 X E[X] + (E[X])^2] =  \\
    E[X^2] - 2 E[X] E[X] + (E[X])^2 = E[X^2] - (E[X])^2.
\end{multline*}
\end{itemize}

## Пример

Пусть функция $f(x)$ задана следующим образом:

$$
f(x) = 
        \begin{cases}
        c(1-x^2), \quad -1 < x < 1 \\
        0, \quad \text{otherwise}
        \end{cases}
$$

1. Найдите корректное значение нормировочной константы $c$, так что $f(x)$ может быть функцией плотности случайной величины $X$.
2. Учитывая полученную константу, найдите математическое ожидание и дисперсию случайной величины $X$.
