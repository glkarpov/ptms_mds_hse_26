---
title: "Теория вероятностей и математическая статистика"
subtitle: "Выборочные распределения. Точечные оценки."
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

## Введение в статистику: визуализация

### Идеальная ситуация: мы знаем параметры и/или характеристики

\begin{center}
\begin{tikzpicture}[scale=1.2]
    % Ось
    \draw[->, thick] (0,0) -- (10,0) node[right] {$\mathbb{R}$};
    
    % Деления на оси
    \foreach \x in {1,2,...,9} {
        \draw (\x,0.1) -- (\x,-0.1) node[below] {\small $\x$};
    }
    
    % Точка E[X]
    \draw[fill=blue] (3,0) circle (2pt) node[above=5pt] {$E[X]$};
    
    % Точка Var[X]
    \draw[fill=red] (6,0) circle (2pt) node[above=5pt] {$Var[X]$};
    
    % Точка theta
    \draw[fill=purple] (8,0) circle (2pt) node[above=5pt] {$\theta$};
\end{tikzpicture}
\end{center}

### Реальная ситуация: параметры и/или характеристики неизвестны

\begin{center}
\begin{tikzpicture}[scale=1.2]
    % Ось
    \draw[->, thick] (0,0) -- (10,0) node[right] {$\mathbb{R}$};
    
    % Деления на оси
    \foreach \x in {1,2,...,9} {
        \draw (\x,0.1) -- (\x,-0.1) node[below] {\small $\x$};
    }
    
    % Серый полупрозрачный фон
    \fill[gray!85, opacity=0.85] (0,-0.5) rectangle (10,0.5);
    
    % Точка E[X] (скрыта в тумане)
    \draw[fill=blue] (3,0) circle (2pt);
    
    % Точка Var[X] (скрыта в тумане)
    \draw[fill=red] (6,0) circle (2pt);
    
    % Точка theta (скрыта в тумане)
    \draw[fill=purple] (8,0) circle (2pt);
    
    
    % Текст о неопределенности
    \node[above=20pt, text width=8cm, align=center] at (5,0) 
        {\small \textcolor{gray!80}{Значения будто скрыты от нас туманом}};
\end{tikzpicture}
\end{center}

- Параметры и характеристики случайной величины — числа, \textbf{точки} на числовой оси.
Семейство методов для угадывания этих значений обычно называется \textbf{точечной оценкой}.


## Случайная выборка и её реализация

\begin{itemize}
    \item Собранные данные обычно называются выборкой, но в статистике мы одновременно имеем дело с двумя различными типами выборок.
    \item Случайная выборка — это вектор (коллекция, набор, совокупность) независимых и одинаково распределенных (i.i.d.) случайных величин:
    $$
        \mathcal{X} = (X_1, \, X_2, \, \ldots, X_n), \quad f_{X_i}(x) = f_{X_j}(x), \; \forall i,j \in [1, \, n], \, \forall x.
    $$
    
    \item Реализация случайной выборки — это набор наблюдений из случайной выборки $\mathcal{X}$, набор конкретных чисел:
    $$
        \mathcal{x} = (x_1, \, x_2, \, \ldots, x_n).
    $$
    
    \item Генеральная совокупность (популяция) — полное множество объектов, обладающих интересующим признаком, несущих реализацию интересующей нас случайной величины. Извлекая наблюдения из генеральной совокупности, мы можем сформировать реализацию выборки.
    
\end{itemize}

## Выборочные распределения

- Пусть $\mathcal{X} = (X_1, \ldots, X_n)$ — случайная выборка со средним $\mu = E[X_i]$ и дисперсией $\sigma^2 = Var[X_i] < \infty$.

- Возможная статистика — это, например, рассмотренная ранее сумма всех элементов $S_n = \sum \limits_{i=1}^{n} X_i$. Её характеристики: $E[S_n] = n \mu$, $Var[S_n] = n \sigma^2$

- Одна из самых важных статистик — выборочное среднее:
$$
    \bar{X} = \frac{X_1+ \ldots + X_n}{n} = \frac{1}{n}\sum\limits_{i=1}^{n} X_i
$$

- Характеристики выборочного среднего $\bar{X}$:
    \begin{itemize}
        \item $E[\bar{X}] = E \left[ \frac{X_1}{n} + \ldots + \frac{X_n}{n} \right]= \dfrac{1}{n} E \left[ X_1 + \ldots + X_n\right] = \frac{n \mu}{n} = \mu$
        \item $\text{Var} \left[ \bar{X} \right] = \text{Var} \left[ \frac{X_1}{n} + \ldots + \frac{X_n}{n} \right]= \dfrac{1}{n^2} \text{Var} \left[ X_1 + \ldots + X_n\right] = \frac{n \sigma^2}{n^2} = \frac{\sigma^2}{n}$
    \end{itemize}

- При выполнении условий ЦПТ ($n \geq 30$) можем заявлять, что:
$$
    \bar{X} \sim \mathcal{N} \left( \mu, \frac{\sigma^2}{n} \right)
$$

## Распределение $\Chi^2$ (хи-квадрат)

\begin{itemize}
    \item Пусть $Z_1, \ldots, Z_k$ — независимые стандартные нормальные случайные величины: $Z_i \sim \mathcal{N}(0,1)$.
    
    \item Определим новую случайную величину:
    $$
    \chi^2(k) = \sum_{i=1}^{k} Z_i^2
    $$
    
    \item Распределение такой случайной величины называется \textbf{распределением хи-квадрат}.
    
    \item Это распределение играет важную роль в статистических процедурах.
\end{itemize}

## Степени свободы

\begin{itemize}
    \item Функция плотности распределения хи-квадрат \textbf{критично зависит} от числа слагаемых $k$ в сумме.
    
    \item Число слагаемых $k$ называется \textbf{степенями свободы} (degrees of freedom, df).
    
    \item Правильное обозначение: $\chi^2(k)$ — читается как "хи-квадрат распределение с $k$ степенями свободы".
\end{itemize}

## Функция плотности распределения хи-квадрат

![Изменение формы функции плотности с изменением числа степеней свободы](../files/chi_square_density.pdf)

## Математическое ожидание и дисперсия распределения хи-квадрат

\begin{itemize}
    \item Если $Y \sim \chi^2(k)$, то:
    $$
    E[Y] = k, \quad \text{Var}(Y) = 2k
    $$
    
    \item Доказательство для $E[Y]$:
    
    Поскольку $Y = \sum_{i=1}^{k} Z_i^2$, где $Z_i \sim \mathcal{N}(0,1)$ независимы:
    $$
    E[Y] = \sum_{i=1}^{k} E[Z_i^2] = \sum_{i=1}^{k} \left(\text{Var}(Z_i) + (E[Z_i])^2 \right)= \sum_{i=1}^{k} (1 + 0) = k
    $$
\end{itemize}
  

## Свойство суммы отклонений от среднего

:::{.callout-theorem}
Пусть $X_1, \ldots, X_k$ — случайная выборка из некоторой генеральной совокупности. Тогда:
$$
\sum_{i=1}^{k} (X_i - \bar{X}) = 0
$$
где $\bar{X} = \frac{1}{k}\sum_{i=1}^{k} X_i$ — выборочное среднее.
:::

## Свойство суммы отклонений от среднего

:::{.callout-proof}
\begin{align*}
\sum\limits_{i=1}^{k} \Bigl(X_i - \bar{X}\Bigr) &= \sum\limits_{i=1}^{k} \Bigl( X_i \Bigr) - k\bar{X} \\
&= \sum\limits_{i=1}^{k} X_i - k \frac{\sum\limits_{i=1}^{k} X_i}{k} \\
&= \sum\limits_{i=1}^{k} X_i - \sum\limits_{i=1}^{k} X_i = 0
\end{align*}
:::



## Теорема о $k\bar{Z}^2$

:::{.callout-theorem}
Пусть $Z_1, \ldots, Z_k$ — случайная выборка из стандартного нормального распределения, т.е. $Z_i \sim \mathcal{N}(0,1)$.

Тогда случайная величина $k\bar{Z}^2$ имеет распределение хи-квадрат с одной степенью свободы:
$$
k\bar{Z}^2 \sim \chi^2(1)
$$
:::

## Теорема о $k\bar{Z}^2$

:::{.callout-proof}
\begin{itemize}

    \item Характеристики:
    $$
    E[\bar{Z}] = \frac{1}{k}\sum_{i=1}^{k} E[Z_i] =  0, \quad \text{Var}[\bar{Z}] = \frac{1}{k^2}\sum_{i=1}^{k} \text{Var}[Z_i] = \frac{1}{k^2} k = \frac{1}{k}
    $$
    
    \item По свойству устойчивости, как сумма независимых нормальных случайных величин, $\bar{Z} \sim \mathcal{N}\left(0, \frac{1}{k}\right)$

    \item Далее рассмотрим случайную величину $\sqrt{k} \bar{Z}$:
    $$
    E[\sqrt{k} \bar{Z}] = 0, \quad \text{Var}(\sqrt{k} \bar{Z}) = k \text{Var}(\bar{Z}) = k \frac{1}{k} = 1
    $$

    \item Значит, $\sqrt{k} \bar{Z} \sim \mathcal{N}(0,1)$ — имеет стандартное нормальное распределение. Поэтому одна такая величина в квадрате будет распределена как хи-квадрат:
    $$
        (\sqrt{k} \bar{Z})^2 = k\bar{Z}^2 \sim \chi^2(1)
    $$
\end{itemize}
:::


## Разложение суммы квадратов

\begin{itemize}
    \item Рассмотрим преобразование:
    
    \begin{align*}
    \sum_{i=1}^{k} Z_i^2 &= \sum\limits_{i=1}^{k} \Bigl[ (Z_i - \bar{Z} + \bar{Z})^2 \Bigr] =  \sum\limits_{i=1}^{k} \Bigl[ \left( \colorbox{green!20}{$(Z_i - \bar{Z})$} + \colorbox{red!20}{$\bar{Z}$} \right)^2 \; \Bigr] \\
    &= \sum_{i=1}^{k} \Bigl[\colorbox{green!20}{$(Z_i - \bar{Z})^2$} + 2\colorbox{green!20}{$(Z_i - \bar{Z})$}\colorbox{red!20}{$\bar{Z}$} + \colorbox{red!20}{$\bar{Z}^2$} \Bigr] \\
    &= \sum_{i=1}^{k} (Z_i - \bar{Z})^2 + 2\bar{Z}\sum_{i=1}^{k}(Z_i - \bar{Z}) +  k\bar{Z}^2
    \end{align*}
    
    \item По свойству суммы отклонений: $\sum\limits_{i=1}^{k}(Z_i - \bar{Z}) = 0$
    
    \item Получаем:
    $$
    \sum_{i=1}^{k} Z_i^2 = \sum_{i=1}^{k} (Z_i - \bar{Z})^2 + k\bar{Z}^2
    $$
\end{itemize}

## Распределение суммы квадратов отклонений

\begin{itemize}
    \item Из разложения:
    $$
    \underbrace{\sum_{i=1}^{k} Z_i^2}_{k \text{ степеней свободы}} = \underbrace{\sum_{i=1}^{k} (Z_i - \bar{Z})^2}_{(k-1) \text{ степеней свободы}} + \underbrace{k\bar{Z}^2}_{1 \text{ степень свободы}}
    $$
    
    \item Известно:
    \begin{itemize}
        \item $\sum \limits_{i=1}^{k} Z_i^2 \sim \chi^2(k)$, и  $k\bar{Z}^2 \sim \chi^2(1)$
    \end{itemize}
    
    \item В итоге получаем, что оставшееся слагаемое имеет $(k-1)$ степень свободы:
    $$
    \boxed{\sum_{i=1}^{k} (Z_i - \bar{Z})^2 \sim \chi^2(k-1)}
    $$

    \item \textbf{Ключевой результат}: Сумма квадратов отклонений от выборочного среднего имеет распределение хи-квадрат с $(k-1)$ степенями свободы. Это фундаментальный результат для статистических тестов и доверительных интервалов.
\end{itemize}

## Выборочная дисперсия

\begin{itemize}
    \item Пусть $X_1, \ldots, X_n$ — случайная выборка из нормального распределения: $X_i \sim \mathcal{N}(\mu, \sigma^2)$.
    
    \item \textbf{Выборочная дисперсия}:
    $$
    s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(X_i - \bar{X})^2
    $$
    
    \item Выборочная дисперсия используется для оценки неизвестной дисперсии генеральной совокупности $\sigma^2$.
\end{itemize}

## Связь выборочной дисперсии с хи-квадрат

\begin{itemize}
    \item Нормализуем наблюдения: $Z_i = \frac{X_i - \mu}{\sigma} \sim \mathcal{N}(0,1)$
    
    \item Тогда выборочное среднее нормализованных величин: $\bar{Z} = \frac{\bar{X} - \mu}{\sigma}$
    
    \item Из предыдущих результатов:
    $$
    \sum_{i=1}^{n} (Z_i - \bar{Z})^2 = \sum_{i=1}^{n} \left(\frac{X_i - \mu}{\sigma} - \frac{\bar{X} - \mu}{\sigma}\right)^2 = \frac{1}{\sigma^2}\sum_{i=1}^{n}(X_i - \bar{X})^2 \sim \chi^2(n-1)
    $$
\end{itemize}

## Распределение выборочной дисперсии

\begin{itemize}
    \item Подставляя определение выборочной дисперсии:
    $$
    \frac{1}{\sigma^2}\sum_{i=1}^{n}(X_i - \bar{X})^2 = \frac{(n-1)s^2}{\sigma^2} \sim \chi^2(n-1)
    $$
    
    \item \textbf{Важный результат}:
    $$
    \boxed{\frac{(n-1)s^2}{\sigma^2} \sim \chi^2(n-1)}
    $$
    
    \item Это означает, что выборочная дисперсия имеет распределение хи-квадрат с $(n-1)$ степенями свободы.
    
    \item \textbf{Математическое ожидание и дисперсия}:
    $$
    E\left[\frac{(n-1)s^2}{\sigma^2}\right] = n-1, \quad \text{Var}\left[\frac{(n-1)s^2}{\sigma^2}\right] = 2(n-1)
    $$
    
    \item \textbf{Следствия для выборочной дисперсии}:
    $$
    E[s^2] = \sigma^2, \quad \text{Var}(s^2) = \frac{2\sigma^4}{n-1}
    $$
\end{itemize}

## Цель точечной оценки

\begin{itemize}
    \item На основе реализации случайной выборки $x_1, x_2, \ldots, x_n$ получить \textbf{предположения} $\hat{\theta}$ о значениях скрытых в тумане реальности параметров.
    
    \item Идея состоит в том, чтобы посчитать значение оценки на реальных имеющихся данных, и чтобы полученное число было бы как можно ближе к истинному значению параметра.
    
    \item Следуя аналогии, мы хотим найти затерянные в тумане точки, путём их угадывания специальным способом, с помощью функции \textbf{оценки}.
\end{itemize}

\begin{center}
\begin{tikzpicture}[scale=1.2]
    % Ось
    \draw[->, thick] (0,0) -- (10,0) node[right] {$\mathbb{R}$};
    
    % Деления на оси
    \foreach \x in {1,2,...,9} {
        \draw (\x,0.1) -- (\x,-0.1) node[below] {\small $\x$};
    }
    
    % Серый полупрозрачный фон (туман неопределенности)
    \fill[gray!85, opacity=0.85] (0,-0.5) rectangle (10,0.5);
    
    % Реальные параметры (скрыты в тумане, без подписей)
    \draw[fill=blue] (3,0) circle (2pt);
    \draw[fill=red] (6,0) circle (2pt);
    \draw[fill=purple] (8,0) circle (2pt);
    
    % Оценки (видны, с подписями)
    \draw[fill=green!70!black] (3.2,0) circle (2pt) node[above=5pt] {\textcolor{green!70!black}{$\hat{\mu}$}};
    \draw[fill=orange!70!black] (5.7,0) circle (2pt) node[above=5pt] {\textcolor{orange!70!black}{$\hat{\sigma}^2$}};
    \draw[fill=purple!70!black] (7.8,0) circle (2pt) node[above=5pt] {\textcolor{purple!70!black}{$\hat{\theta}$}};
        
    % Текст о неопределенности
    \node[above=30pt, text width=9cm, align=center] at (5,0) 
        {\small Значения точечных оценок $\hat{\mu}$, $\hat{\sigma}^2$ и $\hat{\theta}$ "попадают" близко к истинным значениям};
\end{tikzpicture}
\end{center}

## Уже известные точечные оценки
Пусть у нас есть случайная выборка $\mathcal{X} = (X_1, X_2, \ldots, X_n)$ (Независимые, одинаково распределенные) с $\mu \equiv E[X_i]$, $\sigma^2 \equiv Var[X_i]$.

### 1. Выборочное среднее $\bar{X}$
\begin{itemize}
    \item Определение: $\bar{X} = \frac{1}{n}\sum\limits_{i=1}^{n} X_i$
    
    \item Характеристики: $E[\bar{X}] = \mu \; \text{(несмещенная оценка)}, \quad \text{Var}(\bar{X}) = \frac{\sigma^2}{n}$
    
    \item Распределение:
    \begin{itemize}
        \item Если $X_i \sim \mathcal{N}(\mu, \sigma^2)$, то $\bar{X} \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)$
        \item По ЦПТ: при больших $n$ выполняется $\bar{X} \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right)$
    \end{itemize}
\end{itemize}

### 2. Выборочная дисперсия $S^2$

\begin{itemize}
    \item Определение: $S^2 = \frac{1}{n-1}\sum\limits_{i=1}^{n}(X_i - \bar{X})^2$
    
    \item Характеристики: $E[S^2] = \sigma^2 \; \text{(несмещенная оценка)}, \quad \text{Var}(S^2) = \frac{2\sigma^4}{n-1}$
    
    \item Распределение: если $X_i \sim \mathcal{N}(\mu, \sigma^2)$, то:
    $$
    \frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)
    $$
\end{itemize}
