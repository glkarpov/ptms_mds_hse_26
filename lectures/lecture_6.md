---
title: "Теория вероятностей и математическая статистика"
subtitle: "Концепция случайной величины. Дискретные случайные величины."
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

## Случайные величины: Мотивация

\begin{itemize}
\item Элементарный исход в общем может иметь различный характер: цвет, буква, звук и т.д. Но для более углубленного и полного анализа случайного эксперимента лучше работать с числами.
\item Можем ли мы также прикрепить число к каждому элементарному исходу независимо от его природы, а затем оперировать \textbf{только} в пространстве чисел? Спойлер: это даст нам новые инструменты, которые недоступны, если мы работаем с исходами разной природы.
\item Пример: игральная кость с $6$ гранями, $2$ грани желтые, $2$ грани зеленые, $2$ грани черные, без чисел — мы можем искусственно прикрепить числа $1, 2, 3$ к каждому цвету.
\item Результирующее 'прикрепленное' число мы называем случайной величиной.
\end{itemize}

## Случайная величина

::: {.columns}

::: {.column width="65%"}

::: {.callout-definition}
## Определение
Дискретная случайная величина $X$ в пространстве вероятностей $(\Omega, \mathcal{F}, P)$ является отображением $X: \Omega \rightarrow \mathbb{R}$, такое что:
\begin{enumerate}
\item Образ $X(\Omega) = \Omega_X = Im \, X$ (все возможные результаты) является подмножеством $\mathbb{R}$,
\item К конкретному значению $x$ случайной величины $X$ приводят один или несколько элементарных исходов оригинального случайного эксперимента, тем самым, они образуют событие:
$$
\{\omega \in \Omega: X(\omega) = x\} \in \mathcal{F}, \quad \forall  x \in \mathbb{R}
$$

\end{enumerate}
:::

:::

::: {.column width="35%"}
\begin{tikzpicture}[scale=0.55]
    % Рисуем квадратный блок
    \draw[thick, fill=lightgray] (0,0) rectangle (6,6);
    \node[above] at (3,6.2) {$\Omega$};
    
    % Рисуем 9 кругов в сетке 3x3 с цветовой раскраской
    % Круг 1 (левый верхний) - ЗЕЛЕНЫЙ
    \fill[green!70] (1,5) circle (0.8);
    \draw[thick] (1,5) circle (0.8);
    \node[white, font=\bfseries] at (1,5) {$\omega_1$};
    
    % Круг 2 (левый средний) - КРАСНЫЙ
    \fill[red!70] (1,3) circle (0.8);
    \draw[thick] (1,3) circle (0.8);
    \node[white, font=\bfseries] at (1,3) {$\omega_2$};
    
    % Круг 3 (левый нижний) - ОРАНЖЕВЫЙ
    \fill[orange!70] (1,1) circle (0.8);
    \draw[thick] (1,1) circle (0.8);
    \node[white, font=\bfseries] at (1,1) {$\omega_3$};
    
    % Круг 4 (средний верхний) - ЧЕРНЫЙ
    \fill[black!70] (3,5) circle (0.8);
    \draw[thick] (3,5) circle (0.8);
    \node[white, font=\bfseries] at (3,5) {$\omega_4$};
    
    % Круг 5 (средний средний) - ЗЕЛЕНЫЙ
    \fill[green!70] (3,3) circle (0.8);
    \draw[thick] (3,3) circle (0.8);
    \node[white, font=\bfseries] at (3,3) {$\omega_5$};
    
    % Круг 6 (средний нижний) - КРАСНЫЙ
    \fill[red!70] (3,1) circle (0.8);
    \draw[thick] (3,1) circle (0.8);
    \node[white, font=\bfseries] at (3,1) {$\omega_6$};
    
    % Круг 7 (правый верхний) - ЧЕРНЫЙ
    \fill[black!70] (5,5) circle (0.8);
    \draw[thick] (5,5) circle (0.8);
    \node[white, font=\bfseries] at (5,5) {$\omega_7$};
    
    % Круг 8 (правый средний) - ЧЕРНЫЙ
    \fill[black!70] (5,3) circle (0.8);
    \draw[thick] (5,3) circle (0.8);
    \node[white, font=\bfseries] at (5,3) {$\omega_8$};
    
    % Круг 9 (правый нижний) - ЗЕЛЕНЫЙ
    \fill[green!70] (5,1) circle (0.8);
    \draw[thick] (5,1) circle (0.8);
    \node[white, font=\bfseries] at (5,1) {$\omega_9$};
    
    % Целевое пространство справа
    \draw[thick] (8,1) rectangle (10,5);
    \node[above] at (9,5.2) {$\Omega_X$};
    
    % Числа в целевом пространстве
    \node at (9,4.5) {$-500$};
    \node at (9,3.5) {$-50$};
    \node at (9,2.5) {$0$};
    \node at (9,1.5) {$100$};
    
    % Стрелки от каждого цвета к соответствующим числам
    % Красные стрелки (круги 2,6) -> -500
    \draw[->, thick, red] (1.8,3) -- (8,4.5);
    \draw[->, thick, red] (3.2,1) -- (8,4.5);
    
    % Оранжевая стрелка (круг 3) -> -50
    \draw[->, thick, orange] (1.8,1) -- (8,3.5);
    
    % Зеленые стрелки (круги 1,5,9) -> 0
    \draw[->, thick, green] (1.8,5) -- (8,2.5);
    \draw[->, thick, green] (3.2,3) -- (8,2.5);
    \draw[->, thick, green] (5.2,1) -- (8,2.5);
    
    % Черные стрелки (круги 4,7,8) -> 100
    \draw[->, thick, black] (3.2,5) -- (8,1.5);
    \draw[->, thick, black] (5.2,5) -- (8,1.5);
    \draw[->, thick, black] (5.2,3) -- (8,1.5);
\end{tikzpicture}

:::

:::


## Вероятность случайной величины

\begin{itemize}
\item Основной вопрос — как находить вероятности различных значений С.В.
\item Мы знаем, что каждое уникальное значение С.В. привязано к какому-то событию из $\mathcal{F}$. Тогда вероятность этого события и будет вероятностью получить данное значение С.В.
\item Определение. Функция вероятности дискретной случайной переменной $X$ — это функция $P_X(x): \mathbb{R} \rightarrow [0,1]$, заданная как:
$$
P_X(x) = P(X = x) = P(A), \text{ где } A = \{ \omega \in \Omega: X(\omega) = x \}
$$
\item Свойства:
\begin{enumerate}
\item $P_X(x) \geq 0$ для $\forall x \in \Omega_X$, $P_X(x) = 0$ для $x \notin \Omega_X$
\item $\sum \limits_{x_i \in \Omega_X} P_X(x_i) = 1$.
\end{enumerate}
$$
\sum \limits_{x_i \in \Omega_X} P_X(x_i) = \sum \limits_{x_i \in \Omega_X} P \left( \{ \omega \in \Omega: X(\omega) = x_i \}  \right) = P \left( \bigcup \limits_{x_i \in \Omega_X}  \{ \omega \in \Omega: X(\omega) = x_i \} \right) = P \left( \Omega \right) = 1.
$$
\end{itemize}

## Случайные величины: Пример
\vspace{-6.5em}
Подбрасываются две монеты. Первая монета выпадает
орлом с вероятностью $0.6$, вторая с вероятностью $0.7$. 
Предположим, что результаты подбрасываний независимы, и пусть $X$ равно общему количеству выпавших орлов. Постройте дискретную случайную величину и её функцию вероятности. 

## Новое вероятностное пространство

\begin{itemize}
\item Как и прежде, мы можем комбинировать случайные переменные в события.
\item Например, $A = \{ x_1, \ldots, x_k \}$, $x_1, \ldots, x_k \in  \Omega_X$.
\item Для вычисления $P_X(A)$ мы используем принцип аддитивности:
\begin{gather*}
A = \{x_1\} \cup \{x_2\} \cup \ldots \cup \{x_k\} = \bigcup\limits_{i=1}^{k} \{x_i\}\\
P_X(A) = P(\{X = x_1\} \cup \ldots \cup \{X = x_k \}) = \sum \limits_{i=1}^{k} P(\{X = x_i\}).
\end{gather*}
\item В конечном счете, мы можем забыть о нашем оригинальном $(\Omega, \mathcal{F}, P)$, скрыть их «под капотом» нашего случайного эксперимента. Вместо этого мы используем новое пространство $\Omega_X$ всех возможных значений случайной величины $X$ и $P_X(x)$ как новую функцию вероятности.
\end{itemize}

## Функции от случайных величин

- Случайная величина, будучи неизвестным, но все-таки числом, может быть аргументом для какой-либо другой функции,
- Например, если $X$ - это количество проданных тортов, то $Y = cX$ - это доход, где $c$ - цена. Далее, $T = Y - aX - b = kX - b$ может быть чистой прибылью, доход за вычетом издержек на производство. Все это - случайные величины!

- \begin{tikzpicture}
    \draw[thick, fill=blue!10] (0,0) circle (1.0);
    \node at (0,0) {$\Omega_X$};

    \draw[thick, fill=green!10] (4,0) circle (1.0);
    \node at (4,0) {$\Omega_Y$};

    \draw[thick, fill=red!10] (8,0) circle (1.0);
    \node at (8,0) {$\Omega_T$};
  
    \draw[thick, ->] (1.1,0.4) .. controls (2, 0.7) and (2,0.7) .. (2.9,0.4) node[midway, above] {$Y = f(X)$};

    \draw[thick, ->] (5.1,0.4) .. controls (6, 0.7) and (6,0.7) .. (6.9,0.4) node[midway, above] {$T = g(Y)$};
\end{tikzpicture}

## Функции от случайных величин
### Пример

Пусть распределение случайной величины задано таблицей

\begin{center}
    \begin{tabular}{c | c c c c c c} 
        \hline
        $x$ & 0 & -1 & -2 & 1 & 2 & 3\\ [0.5ex] 
        \hline
        $p_X(x)$ & $0.1$ & $0.1$ & $0.1$ & $0.2$ & $0.2$ & $0.3$ \\ 
        \hline
    \end{tabular}
\end{center}

Постройте распределение (функцию вероятности) случайной величины $Y = X^2 + 10$.

## Функции от случайных величин
### Пример

Пусть распределение случайной величины задано таблицей

\begin{center}
    \begin{tabular}{c | c c c c c c} 
        \hline
        $x$ & 0 & -1 & -2 & 1 & 2 & 3\\ [0.5ex] 
        \hline
        $p_X(x)$ & $0.1$ & $0.1$ & $0.1$ & $0.2$ & $0.2$ & $0.3$ \\ 
        \hline
    \end{tabular}
\end{center}

Постройте распределение (функцию вероятности) случайной величины $Y = X^2 + 10$.

Наша задача: восстановить новое пространство элементарных исходов $\Omega_Y$ для величины $Y$ и выразить новую функцию вероятности $P_Y(y)$ через старую известную $P_X(x)$.

\begin{itemize}
\item $P_Y(Y=10) = P_X(\{X=0\}) = 0.1$
\item $P_Y(Y=11) = P_X(\{X=1\} \cup \{X=-1\}) = P_X(\{X=1\}) + P_X(\{X=-1\}) = 0.3$

\item $P_Y(Y=14) = P_X(\{X=2\} \cup \{X=-2\}) = P_X(\{X=2\}) + P_X(\{X=-2\}) = 0.3$

\item $P_Y(Y=19) = P_X(\{X=3\}) = 0.3$

\item \begin{tabular}{c | c c c c} 
         \hline
         $y$ & 10 & 11 & 14 & 19\\ [0.5ex] 
         \hline
         $p_Y(y)$ & $0.1$ & $0.3$ & $0.3$ & $0.3$ \\ 
         \hline
   \end{tabular}
\end{itemize}

## Функции от случайных величин

- Если $Y=g(X)$, то $Y$ это новая случайная величина, со своими характеристиками, со своими возможными значениями $\Omega_Y$, и со своей функцией вероятности $P_Y(y)$.

- :::{.callout-tip title="Построение новой функции вероятности"}
Если $Y=g(X)$, функцию вероятности для $Y$ можно выразить через функцию вероятности для $X$:
$$
P_Y(y) = P(Y=y) = P(g(X) = y) = P(\{ X \in g^{-1}(y) \}) = \sum \limits_{x \in g^{-1}(y)} P(X = x)
$$
:::

- Можно расширить предыдущую картинку и в каком-то смысле говорить, что функция от случайной величины порождает абсолютно новый случайный эксперимент с новым вероятностным пространством (тройкой Колмогорова):
\begin{tikzpicture}
    \draw[thick, fill=blue!10] (0,0) circle (1.0);
    \node at (0,0) {$\Omega_X, \mathcal{F}_X, P_X$};

    \draw[thick, fill=green!10] (4,0) circle (1.0);
    \node at (4,0) {$\Omega_Y, \mathcal{F}_Y, P_Y$};

    \draw[thick, fill=red!10] (8,0) circle (1.0);
    \node at (8,0) {$\Omega_T, \mathcal{F}_T, P_T$};
  
    \draw[thick, ->] (1.1,0.4) .. controls (2, 0.7) and (2,0.7) .. (2.9,0.4) node[midway, above] {$Y = f(X)$};

    \draw[thick, ->] (5.1,0.4) .. controls (6, 0.7) and (6,0.7) .. (6.9,0.4) node[midway, above] {$T = g(Y)$};
\end{tikzpicture}

## Физическое \cancel{Лирическое} отступление

-
\begin{tikzpicture}[scale=1.4]
    % Ось X
    \draw[thick, ->] (-0.5, -0.5) -- (3, -0.5) node[right] {$X$};
    
    % Деления на оси
    \foreach \x in {0, 1, 2} {
        \draw (\x, -0.4) -- (\x, -0.6) node[below] {\x};
    }
    
    % Стержень
    \draw[very thick, gray] (0, 0) -- (2, 0);
    
    % Левая масса в координате 0
    \draw[thick, fill=blue!20] (0, 0) circle (0.3);
    \node at (0, 0) {0.5 кг};
    
    % Правая масса в coordinate 2
    \draw[thick, fill=blue!20] (2, 0) circle (0.3);
    \node at (2, 0) {0.5 кг};
\end{tikzpicture}

-
\begin{tikzpicture}[scale=1.4]
    % Ось X
    \draw[thick, ->] (-0.5, -0.5) -- (3, -0.5) node[right] {$X$};
    
    % Деления на оси
    \foreach \x in {0, 1, 2} {
        \draw (\x, -0.4) -- (\x, -0.6) node[below] {\x};
    }
    
    % Стержень
    \draw[very thick, gray] (0, 0) -- (2, 0);
    
    % Левая масса в координате 0
    \draw[thick, fill=blue!20] (0, 0) circle (0.25);
    \node at (0, 0.35) {0.4 кг};
    
    % Правая масса в coordinate 2
    \draw[thick, fill=blue!20] (2, 0) circle (0.35);
    \node at (2, 0) {0.6 кг};
\end{tikzpicture}

## Физическое \cancel{Лирическое} отступление

\begin{tikzpicture}[scale=1.4]
\draw[thick, ->] (-0.5, -0.5) -- (3, -0.5) node[right] {$X$};

\foreach \x in {0, 1, 2} {
    \draw (\x, -0.4) -- (\x, -0.6) node[below] {\x};
}

\draw[very thick, gray] (0, 0) -- (2, 0);

\draw[thick, fill=blue!20] (0, 0) circle (0.25);
\node at (0, 0.35) {0.4 кг};

\draw[thick, fill=blue!20] (2, 0) circle (0.35);
\node at (2, 0) {0.6 кг};

\draw[thick, fill=red!30] (1.2, -0.1) -- (1.1, -0.3) -- (1.3, -0.3) -- cycle;
\node[below] at (1.2, -0.5) {ЦТ};
\end{tikzpicture}

- $x_{gc} = \sum\limits_{i} x_i m_i$, при $\sum\limits_{i} m_i = 1$.

- В данном примере $x_{gc} = 0 \cdot 0.4 + 2 \cdot 0.6 = 1.2$ 

- Предположим С.В., которую мы реализуем $10^5$ раз с $P_X(0) = 0.4$, $P_X(2) = 0.6$. Посчитаем среднее суммы за все испытания:
$$
    avg = \frac{\approx 60000 \cdot 2 + \approx 40000 \cdot 0}{10^5} \approx 1.2
$$

## Характеристики случайной величины
### Математическое ожидание

\begin{itemize}
\item Математическое ожидание — это число, константа, которое помогает нам понять тренд значений, куда в среднем стремятся значения случайной величины на большой дистанции.
\item Можно рассматривать это как средний результат множества реализаций данного случайного эксперимента.
\item Ожидаемое значение может не входить в набор возможных значений $\Omega_X$.
\end{itemize}

:::{.callout-definition}
Если $X$ — дискретная случайная величина, то ожидание $X$ обозначается как $E[X]$ и определяется как:
$$
E[X] = \sum \limits_{x \in \Omega_X} x P(X = x) = \sum \limits_{x \in \Omega_X} x P_X(x).
$$
:::


## Характеристики случайной величины
### Математическое ожидание

::: {.columns}

::: {.column width="50%"}
**В физическом мире**:

\begin{tikzpicture}[scale=1.4]
\draw[thick, ->] (-0.5, -0.5) -- (4, -0.5) node[right] {$X$};

\foreach \x in {0, 1, 2, 3} {
    \draw (\x, -0.4) -- (\x, -0.6) node[below] {\x};
}

\draw[very thick, gray] (0, 0) -- (3, 0);

\draw[thick, fill=blue!20] (0, 0) circle (0.2);
\node at (0, 0.35) {0.2 кг};

\draw[thick, fill=blue!20] (1, 0) circle (0.3);
\node at (1, 0.45) {0.5 кг};

\draw[thick, fill=blue!20] (3, 0) circle (0.25);
\node at (3, 0.4) {0.3 кг};

\draw[thick, fill=red!30] (1.4, -0.1) -- (1.3, -0.3) -- (1.5, -0.3) -- cycle;
\node[below] at (1.4, -0.5) {ЦТ};
\end{tikzpicture}

$x_{gc} = \sum x_i m_i = 0 \cdot 0.2 + 1 \cdot 0.5 + 3 \cdot 0.3 = 1.4$
:::

::: {.column width="50%"}
**В вероятностном мире**:
\begin{tabular}{c | c c c} 
        \hline
        $x$ & 0 & 1 & 3\\ [0.5ex] 
        \hline
        $p_X(x)$ & $0.2$ & $0.5$ & $0.3$ \\ 
        \hline
\end{tabular}

\vspace{4.2em}
$E[X] = \sum x_i \cdot P_X(X=x_i) = 0 \cdot 0.2 + 1 \cdot 0.5 + 3 \cdot 0.3 = 1.4$
:::
:::

::: {.callout-tip title="Fun facts"}
В международной литературе функция вероятности дискретной случайной величины $P_X(x)$ называется Probability **Mass** Function, своим названием явно подчеркивая аналогию, что вероятность может выступать в роли "массы" элементарного исхода. Тогда математическое ожидание можно интерпретировать как взвешенную сумму всех исходов, где в качестве веса используется вероятность.
:::
