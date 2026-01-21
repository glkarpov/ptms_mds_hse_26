---
title: "Теория вероятностей и математическая статистика"
subtitle: "Условная вероятность. Независимость событий."
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

## Мыслительный эксперимент

\begin{tikzpicture}
    % Рисуем квадратный блок
    \draw[thick, fill=lightgray] (0,0) rectangle (6,6);
    
    % Рисуем 9 кругов в сетке 3x3 с нумерацией по столбцам
    % Круг 1 (левый верхний)
    \fill[white] (1,5) circle (0.8);
    \draw[thick] (1,5) circle (0.8);
    \node at (1,5) {$1$};
    
    % Круг 2 (левый средний)
    \fill[white] (1,3) circle (0.8);
    \draw[thick] (1,3) circle (0.8);
    \node at (1,3) {2};
    
    % Круг 3 (левый нижний)
    \fill[white] (1,1) circle (0.8);
    \draw[thick] (1,1) circle (0.8);
    \node at (1,1) {3};
    
    % Круг 4 (средний верхний)
    \fill[white] (3,5) circle (0.8);
    \draw[thick] (3,5) circle (0.8);
    \node at (3,5) {4};
    
    % Круг 5 (средний средний)
    \fill[white] (3,3) circle (0.8);
    \draw[thick] (3,3) circle (0.8);
    \node at (3,3) {5};
    
    % Круг 6 (средний нижний)
    \fill[white] (3,1) circle (0.8);
    \draw[thick] (3,1) circle (0.8);
    \node at (3,1) {6};
    
    % Круг 7 (правый верхний)
    \fill[white] (5,5) circle (0.8);
    \draw[thick] (5,5) circle (0.8);
    \node at (5,5) {7};
    
    % Круг 8 (правый средний)
    \fill[white] (5,3) circle (0.8);
    \draw[thick] (5,3) circle (0.8);
    \node at (5,3) {8};
    
    % Круг 9 (правый нижний)
    \fill[white] (5,1) circle (0.8);
    \draw[thick] (5,1) circle (0.8);
    \node at (5,1) {9};
\end{tikzpicture}

## Мыслительный эксперимент

\begin{tikzpicture}
    % Рисуем квадратный блок
    \draw[thick, fill=lightgray] (0,0) rectangle (6,6);
    
    % Рисуем 9 кругов в сетке 3x3 с нумерацией по столбцам
    % Круг 1 (левый верхний)
    \fill[white] (1,5) circle (0.8);
    \draw[thick] (1,5) circle (0.8);
    \node at (1,5) {1};
    \fill[green!80!black] (1,5) circle (0.15); % Зеленая точка
    
    % Круг 2 (левый средний)
    \fill[white] (1,3) circle (0.8);
    \draw[thick] (1,3) circle (0.8);
    \node at (1,3) {2};
    \fill[green!80!black] (1,3) circle (0.15); % Зеленая точка
    \fill[blue!80!black] (1.2,2.8) circle (0.15); % Синяя точка
    
    % Круг 3 (левый нижний)
    \fill[white] (1,1) circle (0.8);
    \draw[thick] (1,1) circle (0.8);
    \node at (1,1) {3};
    \fill[green!80!black] (1,1) circle (0.15); % Зеленая точка
    \fill[blue!80!black] (1.2,0.8) circle (0.15); % Синяя точка
    
    % Круг 4 (средний верхний)
    \fill[white] (3,5) circle (0.8);
    \draw[thick] (3,5) circle (0.8);
    \node at (3,5) {4};
    \fill[green!80!black] (3,5) circle (0.15); % Зеленая точка
    \fill[red!80!black] (3.2,4.8) circle (0.15); % Красная точка
    
    % Круг 5 (средний средний)
    \fill[white] (3,3) circle (0.8);
    \draw[thick] (3,3) circle (0.8);
    \node at (3,3) {5};
    \fill[red!80!black] (3,3) circle (0.15); % Красная точка
    
    % Круг 6 (средний нижний)
    \fill[white] (3,1) circle (0.8);
    \draw[thick] (3,1) circle (0.8);
    \node at (3,1) {6};
    \fill[orange!90] (3,1) circle (0.15); % Фиолетовая точка
    
    % Круг 7 (правый верхний)
    \fill[white] (5,5) circle (0.8);
    \draw[thick] (5,5) circle (0.8);
    \node at (5,5) {7};
    \fill[green!80!black] (5,5) circle (0.15); % Зеленая точка
    \fill[red!80!black] (5.2,4.8) circle (0.15); % Красная точка
    
    % Круг 8 (правый средний)
    \fill[white] (5,3) circle (0.8);
    \draw[thick] (5,3) circle (0.8);
    \node at (5,3) {8};
    \fill[red!80!black] (5,3) circle (0.15); % Красная точка
    
    % Круг 9 (правый нижний)
    \fill[white] (5,1) circle (0.8);
    \draw[thick] (5,1) circle (0.8);
    \node at (5,1) {9};
    \fill[orange!80] (5,1) circle (0.15); % Фиолетовая точка
    
    % Легенда
    \node[right] at (6.5,5) {\textcolor{green!80!black}{$\bullet$} Зеленая группа: 1,2,3,4,7};
    \node[right] at (6.5,4) {\textcolor{red!80!black}{$\bullet$} Красная группа: 4,5,7,8};
    \node[right] at (6.5,3) {\textcolor{blue!80!black}{$\bullet$} Синяя группа: 2,3};
    \node[right] at (6.5,2) {\textcolor{orange!80!black}{$\bullet$} Оранжевая группа: 6,9};
\end{tikzpicture}


## Условная вероятность

\begin{tikzpicture}
    % Левый круг - область определения (пространство событий)
    \draw[thick, fill=blue!10] (0,0) circle (2);
    \node at (0,0) {$\mathcal{F}$};
    
    % Правый круг - область значений (вещественные числа от 0 до 1)
    \draw[thick, fill=green!10] (10,0) circle (1.0);
    \node at (10,0) {$[0,1]$};
    
    % Стрелка от левого к правому кругу (изогнутая)
    \draw[thick, ->] (2.2,1) .. controls (5, 2.5) and (5,2.5) .. (8.8,1) node[midway, above] {$P(X)$};

    \draw[thick, ->] (2.2,0.5) .. controls (5, 1.5) and (5,1.5) .. (8.8,0.5) node[midway, above] {$P(X|A)$};

    \draw[thick, ->] (2.2,0) .. controls (5, 0) and (5,0) .. (8.8,0) node[midway, above] {$P(X|B)$};

    \draw[thick, ->] (2.2,-0.5) .. controls (5, -1.5) and (5,-1.5) .. (8.8,-0.5) node[midway, above] {$P(X|C)$};

    \draw[thick, ->] (2.2,-1) .. controls (5, -2.5) and (5,-2.5) .. (8.8,-1) node[midway, above] {$\vdots$};
\end{tikzpicture}

## Условная вероятность
- :::{.callout-definition}
Условная вероятность пересчитывается через обычную вероятность в виде:
$$
    P(A | B) = \frac{P(A \cap B)}{P(B)}
$$
:::

- :::{.callout-tip title="Формула Байеса"}
$$
    P(A | B) = \frac{P(B | A) \cdot P(A)}{P(B)}
$$
:::

## Условная вероятность
При каждом зафиксированном значении параметра (условия) $P(X|K)$ - отдельная самостоятельная вероятностная функция. Для каждой справедливы указанные ранее свойства:

\begin{itemize}
\item $\forall X, K \in \mathcal{F}: \; \; 0 \leq P(X|K) \leq 1$
\item $\forall K \in \mathcal{F}: \; \; P(\Omega|K) = 1$. Easy to show: $P(\Omega|K) = \frac{P(\Omega \cap K)}{P(K)} = (K \subseteq \Omega) = \frac{P(K)}{P(K)} = 1$
\item Аддитивность вероятности:
$$
    \forall X, \, Y, \, K \in \mathcal{F}: \, X \cap Y = \varnothing, \, P\left((X \cup Y) | K \right) = P(X|K) + P(Y|K)
$$
\end{itemize}

## Независимость событий

::: {.columns}
::: {.column width="60%"}
\begin{tikzpicture}
    \draw[thick, fill=lightgray] (0,0) rectangle (6,4);

    % Круг 1
    \fill[white] (1,3) circle (0.6);
    \draw[thick] (1,3) circle (0.6);
    \node at (1,3) {$\omega_1$};
    \fill[green!80!black] (1.3,3) circle (0.12);

    % Круг 2
    \fill[white] (1,1) circle (0.6);
    \draw[thick] (1,1) circle (0.6);
    \node at (1,1) {$\omega_2$};
    \fill[green!80!black] (1.3,1) circle (0.12);

    % Круг 3
    \fill[white] (3,3) circle (0.6);
    \draw[thick] (3,3) circle (0.6);
    \node at (3,3) {$\omega_3$};
    \fill[green!80!black] (3.3,3.2) circle (0.12);
    \fill[red!80!black] (3.3,2.8) circle (0.12);

    % Круг 4
    \fill[white] (3,1) circle (0.6);
    \draw[thick] (3,1) circle (0.6);
    \node at (3,1) {$\omega_4$};
    \fill[green!80!black] (3.3,1.2) circle (0.12);
    \fill[red!80!black] (3.3,0.8) circle (0.12);

    % Круг 5
    \fill[white] (5,3) circle (0.6);
    \draw[thick] (5,3) circle (0.6);
    \node at (5,3) {$\omega_5$};
    \fill[red!80!black] (5.3,3) circle (0.12);

    % Круг 6
    \fill[white] (5,1) circle (0.6);
    \draw[thick] (5,1) circle (0.6);
    \node at (5,1) {$\omega_6$};
    \fill[red!80!black] (5.3,1.2) circle (0.12);
    \fill[blue!80!black] (5.3,0.8) circle (0.12);

    % Круг 7
    \fill[white] (2,2) circle (0.6);
    \draw[thick] (2,2) circle (0.6);
    \node at (2,2) {$\omega_7$};

    % Круг 8
    \fill[white] (4,2) circle (0.6);
    \draw[thick] (4,2) circle (0.6);
    \node at (4,2) {$\omega_8$};
    \fill[blue!80!black] (4.3,2) circle (0.12);

    % Легенда
    \node[above] at (1,4.5) {\textcolor{green!80!black}{$\bullet$} $G = \{ 1, \,2, \, 3, \,4 \}$};
    \node[above] at (4,4.5) {\textcolor{red!80!black}{$\bullet$} $R = \{ 3, \,4, \, 5, \,6 \}$};
    \node[above] at (6.5,4.5) {\textcolor{blue!80!black}{$\bullet$} $B = \{ 6, \,8 \}$};
\end{tikzpicture}
:::

::: {.column width="40%"}
* $P(G) = 0.5$, $P(R) = 0.5$, $P(B) = 0.25$

:::{.callout-question}
$P(R|B), \, P(B|R) = ?$
:::

*  $P(R|B) = 0.5, \, P(B|R) = 0.25$


:::
:::
\begin{itemize}
\item Наблюдаем: $P(B) = P(B|R)$, $P(R) = P(R|B)$. Коэффициент ожидания этих событий a.k.a. вероятность не зависит от того, происходит ли одновременно другое событие или нет. Мы называем такие события \textbf{независимыми}.
\item Более формально, чтобы называть $A$ и $B$ независимыми, должно выполняться:
$$
    P(A | B) = P(A) \text{ И } P(B | A) = P(B), \text{ при } P(A), \, P(B) > 0.
$$
\end{itemize}

## Независимость событий

* Если немного поработаем с идеей о независимости, получим более удобное определение:
$$
    P(A) = P(A|B) = \frac{P \left( A \cap B \right)}{P(B)} \longrightarrow P \left( A \cap B \right) = P(A) \cdot P(B)
$$

:::{.callout-definition}
События $A$ и $B$ из одного вероятностного пространства $\left(\Omega, \mathcal{F}, P \right)$ называются \textit{независимыми}, если:
$$
    P \left( A \cap B \right) = P(A) \cdot P(B), \text{ при } P(A), \, P(B) > 0.
$$
и зависимыми в обратном случае, если таковое равенство не выполняется.
:::

## Показательные задачи
\vspace{-2cm}
### Пример 1
Бросаются два кубика. Какова условная вероятность того, что хотя бы на одном из них выпало 6, при условии, что значения на кубиках различны?

## Показательные задачи
\vspace{-2cm}
### Пример 2
Бросаются два кубика. Какова условная вероятность того, на первом кубике выпало $4$, при условии, что сумма значений $6$? Какова условная вероятность того, на первом кубике выпало $4$, при условии, что сумма значений $7$?

## Слайд для записей
