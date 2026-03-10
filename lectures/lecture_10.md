---
title: "Теория вероятностей и математическая статистика"
subtitle: "Линейные комбинации случайных величин. Ковариация и корреляция."
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
        incremental: true
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---

## Линейная комбинация случайных величин
### Математическое ожидание комбинации

\begin{itemize}
    \item Часто важно анализировать поведение суммы двух или более случайных величин
    \item В основном мы хотим понять, как ведет себя переменная $T = aX \pm bY$, каковы ее характеристики.
    \item Линейное свойство математического ожидания: $E[aX \pm bY] = a E[X] \pm b E[Y]$.
\begin{align*}
    E[T] = & \sum \limits_{i=1}^{n} \sum \limits_{j=1}^{m} (a x_i \pm b y_j) P(X = x_i, Y = y_j) = \\
    & \sum \limits_{i=1}^{n} \sum \limits_{j=1}^{m} a x_i P(X = x_i, Y = y_j)  \pm \sum \limits_{i=1}^{n} \sum \limits_{j=1}^{m} b y_j P(X = x_i, Y = y_j) = \\
    & a \sum \limits_{i=1}^{n} x_i \underset{\text{marginal for } X}{\colorbox{green!20}{$\sum \limits_{j=1}^{m} P(X = x_i, Y = y_j)$}}  \pm b \sum \limits_{j=1}^{m} y_j \underset{\text{marginal for } Y}{\colorbox{red!20}{$\sum \limits_{i=1}^{n} P(X = x_i, Y = y_j)$}} = \\
    & a \sum \limits_{i=1}^{n} x_i \colorbox{green!20}{$P(X=x_i)$} \pm b \sum \limits_{j=1}^{m} y_j \colorbox{red!20}{$P(Y=y_j)$} = a E[X] \pm b E[Y]
\end{align*}
\end{itemize}

## Линейная комбинация случайных величин
### Но дисперсия - это уже совсем другая история...

\begin{itemize}
\item Нас интересует $Var[T] = Var[aX \pm bY]$. 

\item Давайте применим сокращенную формулу для дисперсии:
\begin{align*}
    Var[T] & = E[T^2] - (E[T])^2 = \colorbox{magenta!20}{$E[(aX \pm bY)^2]$} - (aE[X] \pm bE[Y])^2 \\
    & = \colorbox{magenta!20}{$E[a^2 X^2 \pm 2abXY + b^2 Y^2]$} - \left((aE[X])^2 \pm 2abE[X]E[Y] + (bE[Y])^2 \right) \\
    & = \colorbox{green!20}{$a^2 E[X^2]$} \pm 2abE[XY] + \colorbox{red!20}{$b^2 E[Y^2]$} - \colorbox{green!20}{$a^2(E[X])^2$} \mp 2abE[X]E[Y] - \colorbox{red!20}{$b^2(E[Y])^2$} \\
    & = \colorbox{green!20}{$a^2 Var[X]$} + \colorbox{red!20}{$b^2 Var[Y]$} \pm 2ab \biggl(E[XY] - E[X]E[Y] \biggr) 
\end{align*}

\item В процессе использовали свойство линейности математического ожидания.
\item Слагаемое $E[XY] - E[X]E[Y]$ называется \textbf{ковариацией} $X$ и $Y$.
\end{itemize}

## Ковариация и независимость

\textbf{Утверждение:} Если $X$ и $Y$ - независимые случайные величины, то $E[XY] = E[X]E[Y]$

:::{.callout-proof}
Используем определение независимости величин:
\begin{equation*}
    \forall x_i, \; \forall y_j: \; P_X \left( X=x_i \right) P_Y \left( Y = y_j \right) = P(\{X=x_i \} \cap \{ Y=y_j\}) = P \left( X=x_i, Y=y_j \right)
\end{equation*}
\begin{align*}
    E[XY] &= \sum \limits_{i=1}^{n} \sum \limits_{j=1}^{m} x_i y_j P(X = x_i, Y = y_j) = \sum \limits_{i=1}^{n} \sum \limits_{j=1}^{m} x_i y_j P_X(x_i) P_Y(y_j) \\ &= \sum \limits_{i=1}^{n} x_i P_X(x_i) \sum \limits_{j=1}^{m} y_j P_Y(y_j) = E[X] E[Y].
\end{align*}
:::

Будьте внимательны: обратное утверждение неверно!

## Корреляция

\begin{itemize}
\item Ковариация не является хорошей мерой зависимости, поскольку она зависит от масштабов $X$ и $Y$.
\item Идея: нормализовать ковариацию и избавиться от масштабов.
\item Корреляция:
$$
    Corr(X,Y) = \frac{Cov(X,Y)}{\sqrt{Var[X]Var[Y]}}
$$

\item Она строго ограничена от $-1$ до $1$ и:
\begin{align*}
    Corr(X,Y) = 1 & \leftrightarrow Y = kX + b, \; k > 0 \\
    Corr(X,Y) = -1 & \leftrightarrow Y = -kX + b, \; k > 0
\end{align*}

\item Важно: Если переменные независимы, то их ковариация (и корреляция) равна нулю. Обратное утверждение НЕВЕРНО. Очень может быть, что ковариция равна нулю, но при этом величины являются зависимыми
\end{itemize}

## Пример:

\begin{center}
    \begin{tabular}{c | c c} 
    & \(Y=3\) & \(Y=-3\) \\
    \hline
    \(X=-1\) & $\frac{3}{4}$ & $0$ \\
    \(X=2\) & $0$ & $\frac{1}{4}$ \\
\end{tabular}
\end{center}

\begin{enumerate}
    \item Найдите маргинальные функции вероятности для $X$ и $Y$.
    \item Независимы ли $X$ и $Y$?
    \item Найдите ковариацию (и корреляцию) между $X$ и $Y$.
\end{enumerate}

## Решение задачи

### 1. Маргинальные функции вероятности

Для $X$:
\begin{align*}
P(X=-1) &= \sum\limits_{j} P(X=-1, Y=y_j) = \frac{3}{4} + 0 = \frac{3}{4} \\
P(X=2) &= \sum\limits_{j} P(X=2, Y=y_j) = 0 + \frac{1}{4} = \frac{1}{4}
\end{align*}

Для $Y$:
\begin{align*}
P(Y=3) &= \sum\limits_{i} P(X=x_i, Y=3) = \frac{3}{4} + 0 = \frac{3}{4} \\
P(Y=-3) &= \sum\limits_{i} P(X=x_i, Y=-3) = 0 + \frac{1}{4} = \frac{1}{4}
\end{align*}

## Пример
### Проверка независимости

Проверим условие независимости для пары:
\begin{align*}
P(X=-1, Y=3) &= \frac{3}{4} \quad \text{и} \quad P(X=-1)P(Y=3) = \frac{3}{4} \cdot \frac{3}{4} = \frac{9}{16} \neq \frac{3}{4}
\end{align*}

**Ответ:** $X$ и $Y$ **не независимы**.

## Пример
### Ковариация и корреляция

Сначала найдем математические ожидания:
\begin{align*}
E[X] &= (-1) \cdot \frac{3}{4} + 2 \cdot \frac{1}{4} = -\frac{3}{4} + \frac{1}{2} = -\frac{1}{4} \\
E[Y] &= 3 \cdot \frac{3}{4} + (-3) \cdot \frac{1}{4} = \frac{9}{4} - \frac{3}{4} = \frac{3}{2}
\end{align*}

Теперь найдем $E[XY]$:
\begin{align*}
E[XY] &= (-1) \cdot 3 \cdot \frac{3}{4} + (-1) \cdot (-3) \cdot 0 + 2 \cdot 3 \cdot 0 + 2 \cdot (-3) \cdot \frac{1}{4} \\
&= -\frac{9}{4} + 0 + 0 - \frac{6}{4} = -\frac{15}{4}
\end{align*}

## Пример
Ковариация:
\begin{align*}
Cov(X,Y) &= E[XY] - E[X]E[Y] = -\frac{15}{4} - \left(-\frac{1}{4}\right) \cdot \frac{3}{2} \\
&= -\frac{15}{4} + \frac{3}{8} = -\frac{30}{8} + \frac{3}{8} = -\frac{27}{8}
\end{align*}

Для корреляции найдем дисперсии:
\begin{align*}
E[X^2] &= (-1)^2 \cdot \frac{3}{4} + 2^2 \cdot \frac{1}{4} = \frac{3}{4} + 1 = \frac{7}{4} \\
Var[X] &= E[X^2] - (E[X])^2 = \frac{7}{4} - \left(-\frac{1}{4}\right)^2 = \frac{7}{4} - \frac{1}{16} = \frac{27}{16}
\end{align*}

\begin{align*}
E[Y^2] &= 3^2 \cdot \frac{3}{4} + (-3)^2 \cdot \frac{1}{4} = \frac{27}{4} + \frac{9}{4} = 9 \\
Var[Y] &= E[Y^2] - (E[Y])^2 = 9 - \left(\frac{3}{2}\right)^2 = 9 - \frac{9}{4} = \frac{27}{4}
\end{align*}

## Пример
Корреляция:
\begin{align*}
Corr(X,Y) &= \frac{Cov(X,Y)}{\sqrt{Var[X]Var[Y]}} = \frac{-\frac{27}{8}}{\sqrt{\frac{27}{16} \cdot \frac{27}{4}}} \\
&= \frac{-\frac{27}{8}}{\sqrt{\frac{729}{64}}} = \frac{-\frac{27}{8}}{\frac{27}{8}} = -1
\end{align*}

Корреляция равна $-1$, что означает полную отрицательную линейную зависимость между $X$ и $Y$.

## Пример

Пусть известно распределение случайной величины $U$:
\begin{center}
    \begin{tabular}{c | c c c c} 
       $U$ & $u_1=0$ & $u_2 = \pi/3$ & $\ldots$ & $u_{6} = 5 \pi/3$ \\
       \hline
       $P_U$ &  $\frac{1}{6}$  &   $\ldots$  & $\ldots$ & $\frac{1}{6}$ \\
       \hline     
    \end{tabular}
\end{center}
    
\begin{enumerate}
        \item Введём переменные $X = \cos{U}$ и $Y = \sin{U}$. Постройте таблицу их совместного распределения.
        \item Являются ли они зависимыми? Рассмотрите, например, $P(X = \frac{1}{2})$ и $P(X = \frac{1}{2} \; | \; Y = \frac{\sqrt{3}}{2})$.
        \item Найдите математические ожидания $E[X]$ и $E[Y]$.
        \item Найдите ковариацию и корреляцию между $X$ и $Y$.
\end{enumerate}
