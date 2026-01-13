---
title: "Теория вероятностей и математическая статистика"
subtitle: "Вероятностное пространство. Аксиоматическое определение вероятности."
institute: "ФКН ВШЭ"
author: "Глеб Карпов"
format: 
    beamer:
        pdf-engine: xelatex
        aspectratio: 169
        fontsize: 9pt
        theme: Singapore
        fonttheme: serif
        section-titles: true
        incremental: true
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---
## Андрей Колмогоров меняет всё

\begin{itemize}
\item Строгая формализация через множества: пространство исходов $\Omega$, события — элементы $\mathcal{F}$
\item Аксиоматизация: построение на основе теории меры
\item Три аксиомы для вероятностной функции: неотрицательность, нормировка ($P(\Omega) = 1$), аддитивность
\end{itemize}

## Описание случайного эксперимента
### Пространство элементарных исходов
\begin{itemize}
\item Множество, которое содержит все возможные \textit{уникальные} результаты случайного эксперимента:
$$
    \Omega = \{ \omega_1, \, \omega_2, \, \omega_n, \, \ldots  \}
$$
\item Может быть конечным или бесконечным
\item Критически зависит от установки случайного эксперимента и того, что мы хотим наблюдать и описывать
\end{itemize}

## Описание случайного эксперимента
### Пространство элементарных исходов: примеры

\begin{itemize}
\item Подбрасываются две визуально различимые монеты: $\Omega = \{ Hh, \, Tt, \, Ht, \, Th \}$
\item Подбрасываются две идентичные монеты: $\Omega = \{ 2H, \, 2T, \, Diff\}$
\item Идентичные монеты с внедренным различием: $\Omega = \{ Hh, \, Tt, \, Ht, \, Th \}$
\item Кубик со сторонами-буквами: $\Omega = \{ a, \, b, \, c, \, d, \, e, \, f \}$
\end{itemize}

## Описание случайного эксперимента
### Событие

\begin{itemize}
\item Зачастую нас интересует не конкретный элементарный исход, а набор из нескольких, e.g.  "Если выпадет 2, 3, 6", то мы получим выигрыш
\item Множество, построенное из одного или нескольких элементарных исходом называют \textit{событием}
\item Важное отличие от элементарного исхода: исход случается \textit{один и только один}, событий может случиться одновременно много!
\end{itemize}

::: {.callout-tip title="Важно!"}
 Мы говорим, что *событие произошло*, если реализовался какой-то из элементарных исходов этого события.
:::

## Описание случайного эксперимента
### Пространство событий

\begin{itemize}
\item Множество, которое содержит все возможные \textit{события}, которые можно построить из множества исходов $\Omega$
\item Иными словами, множество всех возможных подмножеств $\Omega$:
$$
    \mathcal{F} = \{ A_1, \, A_2, \, A_n, \, \ldots  \}, \; \forall A_i \subset \Omega
$$
\item Само пространство элементарных исходов тоже событие: $\Omega \subset \Omega$, поэтому $\Omega \in \mathcal{F}$
\end{itemize}

\begin{center}
\begin{tikzpicture}
    % Рисуем круг для множества (справа)
    \draw[thick, fill=blue!10] (3.5,0.5) circle (2.);
    
    % Обозначение множества
    \node[above] at (3.5,2.5) {\small (Пример $\mathcal{F}$: все подмножества $\{a,b,c\}$)};
    
    % Все 8 подмножеств
    \node at (3.5,1.5) {$\{a,b,c\}$};
    \node at (2,1.) {$\{a,b\}$};
    \node at (5,1.) {$\{a,c\}$};
    \node at (3.5,1.) {$\{b,c\}$};
    \node at (2,0) {$\{a\}$};
    \node at (5,0) {$\{b\}$};
    \node at (3.5,0) {$\{c\}$};
    \node at (3.5,-1.) {$\{\varnothing \}$};
    
    % Новый круг слева с общими событиями
    \draw[thick, fill=green!10] (-3.5,0.5) circle (2.);
    
    % Обозначение множества
    \node[above] at (-3.5,2.5) {\small ($\mathcal{F}$, в общем виде)};
    
    % Общие события
    \node at (-3.5,1.5) {$\Omega$};
    \node at (-4.7,1.) {$A_1$};
    \node at (-2.3,1.) {$A_2$};
    \node at (-3.5,1.) {$A_3$};
    \node at (-4.7,0) {$A_k$};
    \node at (-2.3,0) {$A_n$};
    \node at (-3.5,0) {$\vdots$};
    \node at (-3.5,-1.) {$\varnothing$};
\end{tikzpicture}
\end{center}

## Описание случайного эксперимента
### Пространство событий

:::{.callout-question}
Если мощность пространства элементарных исходов $|\Omega| = n$, какая будет мощность пространста событий $|\mathcal{F}|$?
:::


## Описание случайного эксперимента
### Вероятность
\begin{itemize}
\item В конечном счете мы хотим наклеить на каждое событие "бирку" с информацией о том, насколько мы уверены в том, что событие случится
\item Этот коэффициент нашей уверенности решили измерять от $0$ до $1$, его-то и называем *вероятностью*
\item Формально, вероятность представляет собой функцию, которая каждому событию ставит в соответствие число:
$$
    P(X): \, \mathcal{F} \longrightarrow [0,1] \subset \mathbb{R} 
$$
\end{itemize}

\begin{tikzpicture}
    % Левый круг - область определения (пространство событий)
    \draw[thick, fill=blue!10] (0,0) circle (2);
    \node at (0,0) {$\mathcal{F}$};
    
    % Правый круг - область значений (вещественные числа от 0 до 1)
    \draw[thick, fill=green!10] (10,0) circle (1.0);
    \node at (10,0) {$[0,1]$};
    
    % Стрелка от левого к правому кругу (изогнутая)
    \draw[thick, ->] (2.2,0) .. controls (5, 1) and (5,1) .. (8.8,0) node[midway, above] {$P(X)$};
\end{tikzpicture}

## Свойства вероятностной функции
\begin{itemize}
\item $0 \leq P(X) \leq 1, \; \forall X \in \mathcal{F}$
\item $P(\Omega) = 1$, $P(\varnothing) = 0$
\item \textit{Свойство аддитивности вероятности}:
$$
    \forall X, \, Y \in \mathcal{F}: \, X \cap Y = \varnothing, \, P(X \cup Y) = P(X) + P(Y)
$$

Более душно: Если коллекция событий $A_1, \,  A_2, \, \ldots$ - попарно не пересекаются, i.e. $A_i \cap A_j = \varnothing, \, i \neq j$, то:
$$
    P\left(\bigcup_{i=1}^m A_i\right)=\sum_{i=1}^m P\left(A_i\right)
$$
\end{itemize}

## Вероятность
### Комплиментарные события и формула включений исключений
::: {.columns}
::: {.column width="40%"}
\begin{tikzpicture}[scale=1.2]
  % Прямоугольное пространство выборки Ω
  \draw[thick, black] (0,0) rectangle (5,4);
  \node[above] at (3,4) {\Large $\Omega$};
  
  % Событие A (круг слева)
  \draw[thick, blue, fill=blue!20] (1.5,2) circle (1.3);
  \node[blue] at (0.7,2.8) {\Large $A$};
  
  % Событие B (круг справа)
  \draw[thick, red, fill=red!20] (3.5,2) circle (1.0);
  \node[red] at (4.3,2.8) {\Large $B$};
  
  % Пересечение A ∩ B (закрашено более темным цветом)
  \begin{scope}
    \clip (1.5,2) circle (1.3);
    \fill[purple!40] (3.5,2) circle (1.0);
  \end{scope}
  
  % Подпись пересечения
  \node[purple, font=\large] at (3,2) {$A \cap B$};
  
  % Подписи областей
  \node[blue] at (0.4,1.0) {$\Omega \setminus A$};
  \node[red] at (4.6,1.0) {$\Omega \setminus B$};ß
  \node[black] at (0.7,3.5) {$(A \cup B)^c$};
\end{tikzpicture}
:::

::: {.column width="55%"}
\begin{itemize}
\item Свойство: Если $A \in \mathcal{F}$, то $P(A) + P(\Omega \backslash A) = 1$.

События $A$ и $\bar{A} = \Omega \backslash A$ такие, что $A \cap \bar{A} = \varnothing$, и $\Omega = A \cup \bar{A}$, откуда при помощи свойств вероятности получим: $P(\Omega) = P(A \cup \bar{A}) = P(A) + P(\Omega \backslash A) = 1$

\item Формула включений-исключений: Если $A, B \in \mathcal{F}$, то 
$$
    P(A \cup B) = P(A)  + P(B) - P(A \cap B)
$$
Событие $A$ - объединение непересекающихся $A \backslash B$ и $A \cap B$, следовательно $P(A)=P(A \backslash B) + P(A \cap B)$ и симметрично $P(B)=P(B \backslash A) + P(A \cap B)$.
\begin{gather*}
P(A)+P(B) =P(A \backslash B)+2 P(A \cap B)+P(B \backslash A) \\
=P((A \backslash B) \cup(A \cap B) \cup(B \backslash A))+P(A \cap B) \\
=P(A \cup B)+P(A \cap B) .
\end{gather*}


\item Свойство: Если $A, B \in \mathcal{F}$ and $A \subseteq B$, то $P(A) \leq P(B)$.
Показать просто: $P(B) = P(A) + P(B \backslash A) \geq P(A)$.
\end{itemize}
:::
:::
