---
title: "Теория вероятностей и математическая статистика"
subtitle: "Центральная предельная теорема"
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

## Напоминание: Линейная комбинация случайных величин

Предположим, что у нас есть $X$ и $Y$ — две случайные величины. Следующие свойства работают для *любой* возможной природы этих переменных.

\begin{enumerate}
    \item Линейное свойство математического ожидания: $E[aX \pm bY] = a E[X] \pm b E[Y]$.
    \item Дисперсия линейной комбинации: $Var[aX \pm bY] = a^2 Var[X] + b^2 Var[Y] \pm 2ab\biggl(E[XY] - E[X]E[Y]\biggr)$.
    \item Если $X$ и $Y$ независимы: $Var[aX \pm bY] = a^2 Var[X] + b^2 Var[Y]$.
\end{enumerate}

## Иллюстративный пример
### Функция от двух дискретных случайных величин

Предположим, что мы бросаем два $6$-гранных кубика, независимых друг от друга. В итоге мы наблюдаем дискретный случайный вектор $(X,Y)$, где $X$ и $Y$ — случайные величины, соответствующие выпавшим числам на каждом из кубиков.
Поскольку существует $36$ различных пар, совместная функция вероятности задается как: $P(X=x_i, \, Y=y_j) = \frac{1}{36}$.

Введем новую случайную величину $T$ как функцию от $X$ и $Y$: $T = f(X,Y) = X + Y$. Построим функцию вероятности для случайной величины $T$.

## Иллюстративный пример
### Построение функции вероятности для $T = X + Y$

Для каждого значения $t$ случайной величины $T$ найдем все пары $(x,y)$, которые дают в сумме $t$:

\begin{itemize}
    \item $T = 2$: только $(1,1)$
    \item $T = 3$: $(1,2), (2,1)$  
    \item $T = 4$: $(1,3), (2,2), (3,1)$
    \item $T = 5$: $(1,4), (2,3), (3,2), (4,1)$
    \item $T = 6$: $(1,5), (2,4), (3,3), (4,2), (5,1)$
    \item $T = 7$: $(1,6), (2,5), (3,4), (4,3), (5,2), (6,1)$
    \item $T = 8$: $(2,6), (3,5), (4,4), (5,3), (6,2)$
    \item $T = 9$: $(3,6), (4,5), (5,4), (6,3)$
    \item $T = 10$: $(4,6), (5,5), (6,4)$
    \item $T = 11$: $(5,6), (6,5)$
    \item $T = 12$: только $(6,6)$
\end{itemize}

## Иллюстративный пример
### Таблица функции вероятности

\begin{center}
\begin{tabular}{|c|c|c|c|c|c|c|c|c|c|c|c|}
\hline
$t$ & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 \\
\hline
$P(T = t)$ & $\frac{1}{36}$ & $\frac{1}{18}$ & $\frac{1}{12}$ & $\frac{1}{9}$ & $\frac{5}{36}$ & $\frac{1}{6}$ & $\frac{5}{36}$ & $\frac{1}{9}$ & $\frac{1}{12}$ & $\frac{1}{18}$ & $\frac{1}{36}$ \\
\hline
\end{tabular}
\end{center}

### График функции вероятности

\begin{center}
\begin{tikzpicture}[scale=0.8]
% Оси
\draw[->] (0,0) -- (14,0) node[right] {$t$};
\draw[->] (0,0) -- (0,3.5) node[above] {$P(T = t)$};

% Сетка
\draw[gray, very thin] (0,0) grid (14,3.5);

% Подписи осей
\foreach \x in {2,3,4,5,6,7,8,9,10,11,12}
    \draw (\x,0) -- (\x,-0.1) node[below] {\x};

% Столбцы гистограммы
\draw[fill=blue!30] (1.5,0) rectangle (2.5,0.5) node[above, xshift=-0.3cm] {$\frac{1}{36}$};
\draw[fill=blue!30] (2.5,0) rectangle (3.5,1) node[above, xshift=-0.3cm] {$\frac{1}{18}$};
\draw[fill=blue!30] (3.5,0) rectangle (4.5,1.5) node[above, xshift=-0.3cm] {$\frac{1}{12}$};
\draw[fill=blue!30] (4.5,0) rectangle (5.5,2) node[above, xshift=-0.3cm] {$\frac{1}{9}$};
\draw[fill=blue!30] (5.5,0) rectangle (6.5,2.5) node[above, xshift=-0.3cm] {$\frac{5}{36}$};
\draw[fill=red!30] (6.5,0) rectangle (7.5,3) node[above, xshift=-0.3cm] {$\frac{1}{6}$};
\draw[fill=blue!30] (7.5,0) rectangle (8.5,2.5) node[above, xshift=-0.3cm] {$\frac{5}{36}$};
\draw[fill=blue!30] (8.5,0) rectangle (9.5,2) node[above, xshift=-0.3cm] {$\frac{1}{9}$};
\draw[fill=blue!30] (9.5,0) rectangle (10.5,1.5) node[above, xshift=-0.3cm] {$\frac{1}{12}$};
\draw[fill=blue!30] (10.5,0) rectangle (11.5,1) node[above, xshift=-0.3cm] {$\frac{1}{18}$};
\draw[fill=blue!30] (11.5,0) rectangle (12.5,0.5) node[above, xshift=-0.3cm] {$\frac{1}{36}$};
\end{tikzpicture}
\end{center}

### Промежуточный вывод
Мы на очень простом примере можем пронаблюдать, как функция вероятности суммы одинаково распределенных дискретных величин получает "усиление" в центральных значениях, так как к этим элементарным исходам приводят больше комбинаций изначальных величин.

## Центральная предельная теорема
### Предпосылки

\begin{itemize}
    \item Пусть $X_1, X_2, \; \ldots$ — последовательность независимых случайных величин, взятых из одного и того же распределения, т.е. все $X_i$ имеют одинаковое математическое ожидание $E[X] = \mu$, одинаковую дисперсию $Var[X] = \sigma^2 < \infty$. 

    \item Мы конструируем \textbf{новую} случайную величину как частичную сумму первых $n$ случайных величин $X_i$:
    $$
    S_n = \sum \limits_{i=1}^{n} X_i.
    $$

    \item Согласно свойствам математического ожидания и дисперсии, характеристики новой случайной величины:
    \begin{gather*}
        E[S_n] = E \Bigl[ \sum \limits_{i=1}^{n} X_i \Bigr] = \sum \limits_{i=1}^{n} E[X_i] = n \mu \\
        Var[S_n] = Var \Bigl[ \sum \limits_{i=1}^{n} X_i \Bigr] = \sum \limits_{i=1}^{n} Var[X_i] = n \sigma^2
    \end{gather*}
\end{itemize}

## Центральная предельная теорема

\begin{itemize}
    \item \textbf{Центральная предельная теорема}: распределение такой случайной величины $S_n$ стремится к нормальному распределению при $n \rightarrow \infty$: 
    $$
    S_n  \rightarrow  Y \sim \mathcal{N}(n \mu, n \sigma^2)
    $$

    \item Душно:
    $$
      \forall x \in \mathbb{R} \quad  P(S_n < x) \underset{n \rightarrow \infty}{\longrightarrow} P(Y < x), \text{ где } Y \sim \mathcal{N}(n \mu, n \sigma^2),
    $$
    что означает, что в каждой точке $x$ функция распределения $F_{S_n}(x)$ стремится к функции распределения $F_Y(x)$, т.е. они буквально "накладываются" друг на друга и теперь характеризуют одну и ту же случайную величину.

    \item Проще говоря: $S_n \sim \mathcal{N}(n \mu, n \sigma^2)$, когда $n$ достаточно велико.
    \item Обычно "достаточно велико" это $n \geq 30$.
\end{itemize}

## Центральная предельная теорема
### Формулировка через стандартизацию

\begin{itemize}
    \item Проводим операцию стандартизации введенной ранее случайной величины $S_n$:
    $$
    Z_n = \frac{S_n - E[S_n]}{\sqrt{Var[S_n]}} = \frac{S_n - n \mu}{\sigma \sqrt{n}}
    $$

    \item Характеристики:
    \begin{gather*}
    E[Z_n] = E \Biggl[ \frac{S_n - n \mu}{\sigma \sqrt{n}} \Biggr] = E \Biggl[\frac{S_n}{\sigma \sqrt{n}} \Biggr] - E \Biggl[\frac{n \mu}{\sigma \sqrt{n}} \Biggr] = \frac{n \mu}{\sigma \sqrt{n}} - \frac{n \mu}{\sigma \sqrt{n}} = 0 \\
    Var[Z_n] = Var \Biggl[ \frac{S_n - n \mu}{\sigma \sqrt{n}} \Biggr] = Var \Biggl[\frac{S_n}{\sigma \sqrt{n}} \Biggr] + Var \Biggl[\frac{n \mu}{\sigma \sqrt{n}} \Biggr] = \frac{Var[S_n]}{n \sigma^2} + 0 = 1
    \end{gather*}

    \item Тогда говорим, что:
    $$
      \forall x \in \mathbb{R} \quad  P(Z_n < x) \underset{n \rightarrow \infty}{\longrightarrow} P(Z < x), \text{ где } Z \sim \mathcal{N}(0, 1)
    $$
    Или проще: стандартизованная частичная сумма $Z_n \sim \mathcal{N}(0,1)$, когда $n$ достаточно велико.
    
    Обычно требуем $n \geq 30$.
\end{itemize}
