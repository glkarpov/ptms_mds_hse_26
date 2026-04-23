---
title: "Теория вероятностей и математическая статистика"
subtitle: "Нормальное распределение."
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

## В прошлых сериях...
### Физическая аналогия: значение плотности вещества в точке

- Само по себе значение функции плотности $\rho(x_0)$ не обозначает массу в точке $x_0$. Смысл несет именно произведение плотности на длину, вспомним, чтобы сократились размерности $[kg] = \left[\frac{kg}{m}\right] [m]$

\begin{tikzpicture}
    % Верхний график - Рельс :)
    \begin{scope}[yshift=3cm]
        \begin{axis}[
            width=10cm,
            height=2cm,
            xmin=-1, xmax=12,
            ymin=-0.5, ymax=1.5,
            axis lines=center,
            xlabel={$x$},
            ylabel={Объект},
            xtick={0,2,4,6,8,10},
            ytick={0},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем металлическую пластину как прямоугольник
        \addplot[thick, blue, fill=blue!20, fill opacity=0.7] coordinates {
            (0,0) (0,1) (10,1) (10,0) (0,0)
        } \closedcycle;
        
        % Выбираем точку x_0 = 6 и dx = 1 (те же значения что и в нижнем графике)
        \def\xzero{5}
        \def\dx{0.5}
        
        % Зеленая область на металлической пластине (смешивание с синим)
        \addplot[thick, green!80!blue, fill=green!60!blue!40, fill opacity=0.8, domain=\xzero-\dx/2:\xzero+\dx/2, samples=100] {0.1} \closedcycle;
        \addplot[thick, green!80!blue, fill=green!60!blue!40, fill opacity=0.8, domain=\xzero-\dx/2:\xzero+\dx/2, samples=100] {0.9} \closedcycle;
        
        % Вертикальные линии для области dx на пластине
        \draw[thick, green!80!blue] (\xzero-\dx/2,0.1) -- (\xzero-\dx/2,0.9);
        \draw[thick, green!80!blue] (\xzero+\dx/2,0.1) -- (\xzero+\dx/2,0.9);
        
        % Добавляем текстовую метку
        \node[above] at (5,1) {Рельс :)};
        
        \end{axis}
    \end{scope}
    
    % Нижний график - плотность
    \begin{scope}
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.15,
            axis lines=center,
            xlabel={$x$},
            ylabel={Плотность $\rho(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1},
            yticklabels={0,0.1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем функцию плотности без заливки
        \addplot[thick, red, domain=0:10, samples=100] {0.1};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        % Выбираем точку x_0 = 6 и dx = 1
        \def\xzero{5}
        \def\dx{0.5}
        
        % Зеленая область вокруг точки x_0 шириной dx (темнее)
        \addplot[thick, green!80!black, fill=green!60!black!50, fill opacity=0.8, domain=\xzero-\dx/2:\xzero+\dx/2, samples=100] {0.1} \closedcycle;
        
        % Вертикальные линии для области dx
        \draw[thick, green!80!black] (\xzero-\dx/2,0) -- (\xzero-\dx/2,0.1);
        \draw[thick, green!80!black] (\xzero+\dx/2,0) -- (\xzero+\dx/2,0.1);
        
        % Точка x_0
        \draw[thick, green!80!black] (\xzero,0) -- (\xzero,-0.02);
        \node[green!80!black, below] at (\xzero,0) {$x_0$};
        
        % Подписи для dx
        \node[green!80!black, below] at (\xzero-\dx/4,-0.04) {$dx$};
        
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.5cm]
        % Объединенная формула для массы
        \node[draw, fill=gray!10, rounded corners, minimum width=3.5cm, minimum height=1.5cm] at (0.5,1.3) {
            \begin{minipage}{3.3cm}
                \centering
                $dm = \rho(x_0) \cdot dx$\\
                \small Масса кусочка шириной $dx$ около точки $x_0$
            \end{minipage}
        };
                
        % Стрелка к зеленой области
        \draw[thick, green!80!black, ->] (0.17,1.4) -- (-5.9,1.0);
        \node[green!80!black, left] at (-1.8,-0.2) {Масса = $0.1 \cdot 0.5 = 0.05$};
    \end{scope}
    
\end{tikzpicture}

## В прошлых сериях...
### Значение плотности вероятности в точке

- По аналогии с физикой: само по себе значение функции плотности $f_X(x_0)$ не обозначает вероятность в точке $x_0$. Смысл несет именно произведение плотности на длину интервала.

\begin{tikzpicture}
    \begin{scope}
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.15,
            axis lines=center,
            xlabel={$x$},
            ylabel={$f_X(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1},
            yticklabels={0,0.1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем функцию плотности без заливки
        \addplot[thick, red, domain=0:10, samples=100] {0.1};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        % Выбираем точку x_0 = 6 и dx = 1
        \def\xzero{5}
        \def\dx{0.5}
        
        % Зеленая область вокруг точки x_0 шириной dx (темнее)
        \addplot[thick, green!80!black, fill=green!60!black!50, fill opacity=0.8, domain=\xzero-\dx/2:\xzero+\dx/2, samples=100] {0.1} \closedcycle;
        
        % Вертикальные линии для области dx
        \draw[thick, green!80!black] (\xzero-\dx/2,0) -- (\xzero-\dx/2,0.1);
        \draw[thick, green!80!black] (\xzero+\dx/2,0) -- (\xzero+\dx/2,0.1);
        
        % Точка x_0
        \draw[thick, green!80!black] (\xzero,0) -- (\xzero,-0.02);
        \node[green!80!black, below] at (\xzero,0) {$x_0$};
        
        % Подписи для dx
        \node[green!80!black, below] at (\xzero-\dx/4,-0.04) {$dx$};
        
        \end{axis}
    \end{scope}

    \begin{scope}[yshift=-2cm]
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.25,
            axis lines=center,
            xlabel={$x$},
            ylabel={$f_X(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1,0.2},
            yticklabels={0,0.1,0.2},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем переменную плотность (растет к середине, убывает к краям)
        \addplot[thick, red, domain=0:10, samples=100] {0.2 * (1 - (x-5)^2/25)};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Выбираем точку x_0 = 7 и dx = 0.1 для второго графика
        \def\xzero{7}
        \def\dx{0.1}
        
        % Зеленая область вокруг точки x_0 шириной dx (темнее)
        \addplot[thick, green!80!black, fill=green!60!black!50, fill opacity=0.8, domain=\xzero-\dx/2:\xzero+\dx/2, samples=100] {0.2 * (1 - (x-5)^2/25)} \closedcycle;
        
        % Вертикальные линии для области dx
        \draw[thick, green!80!black] (\xzero-\dx/2,0) -- (\xzero-\dx/2,{0.2 * (1 - (\xzero-\dx/2-5)^2/25)});
        \draw[thick, green!80!black] (\xzero+\dx/2,0) -- (\xzero+\dx/2,{0.2 * (1 - (\xzero+\dx/2-5)^2/25)});
        
        % Точка x_0
        \draw[thick, green!80!black] (\xzero,0) -- (\xzero,-0.02);
        \node[green!80!black, below] at (\xzero,0) {$x_0$};
        
        % Подписи для dx
        \node[green!80!black, below] at (\xzero-\dx/4,-0.04) {$dx$};
        
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.5cm]
        % Объединенная формула для массы
        \node[draw, fill=gray!10, rounded corners, minimum width=5.9cm, minimum height=1.5cm] at (0.5,1.3) {
            \begin{minipage}{5.8cm}
                \centering
                $P(X \in (x_0 - \frac{dx}{2}, x_0 + \frac{dx}{2})) = f_X(x_0) \cdot dx$\\
            \end{minipage}
        };
                
        % Стрелка к зеленой области в первом графике
        \draw[thick, green!80!black, ->] (-2.,1.1) -- (-5.9,1.0);
        
        % Стрелка к зеленой области во втором графике (x_0 = 7)
        \draw[thick, green!80!black, ->] (-2.,1.1) -- (-4.7,-1.0);
        
        \node[green!80!black, below] at (0.5,-0.2) {Probability = area =  $f_X(x_0) \cdot dx$};
    \end{scope}
    
\end{tikzpicture}

## В прошлых сериях...
### Вероятность попадания в интервал

- Последовательно складывая такие вероятности попадания в окрестность, получаем площадь под графиком функции плотности от точки $a$ до точки $b$, которая и интерпретируется нами как $P(a<X<b)$.

\begin{tikzpicture}
    \begin{scope}
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.15,
            axis lines=center,
            xlabel={$x$},
            ylabel={$f_X(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1},
            yticklabels={0,0.1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем функцию плотности без заливки
        \addplot[thick, red, domain=0:10, samples=100] {0.1};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        % Определяем параметры для прямоугольных областей
        \def\dx{0.5}
        \def\startx{3}
        
        % Создаем 3 последовательных прямоугольных области
        % Прямоугольник 0 (синий) - от 2.75 до 3.25, высота 0.1
        \def\height{0.1}
        \fill[blue!60, fill opacity=0.8] (2.75,0) rectangle (3.25,\height);
        \draw[thick, blue!80!black] (2.75,0) -- (2.75,\height);
        \draw[thick, blue!80!black] (3.25,0) -- (3.25,\height);
        \draw[thick, blue!80!black] (2.75,\height) -- (3.25,\height);
        \draw[thick, blue!80!black] (3,0) -- (3,-0.02);
        
        % Прямоугольник 1 (зеленый) - от 3.25 до 3.75, высота 0.1
        \fill[green!60, fill opacity=0.8] (3.25,0) rectangle (3.75,\height);
        \draw[thick, green!80!black] (3.25,0) -- (3.25,\height);
        \draw[thick, green!80!black] (3.75,0) -- (3.75,\height);
        \draw[thick, green!80!black] (3.25,\height) -- (3.75,\height);
        \draw[thick, green!80!black] (3.5,0) -- (3.5,-0.02);
        
        % Прямоугольник 2 (красный) - от 3.75 до 4.25, высота 0.1
        \fill[red!60, fill opacity=0.8] (3.75,0) rectangle (4.25,\height);
        \draw[thick, red!80!black] (3.75,0) -- (3.75,\height);
        \draw[thick, red!80!black] (4.25,0) -- (4.25,\height);
        \draw[thick, red!80!black] (3.75,\height) -- (4.25,\height);
        \draw[thick, red!80!black] (4,0) -- (4,-0.02);
        \end{axis}
    \end{scope}

    \begin{scope}[yshift=-2cm]
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.25,
            axis lines=center,
            xlabel={$x$},
            ylabel={$f_X(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1,0.2},
            yticklabels={0,0.1,0.2},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем переменную плотность (растет к середине, убывает к краям)
        \addplot[thick, red, domain=0:10, samples=100] {0.2 * (1 - (x-5)^2/25)};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Определяем параметры для прямоугольных областей (второй график)
        \def\dx{0.3}
        \def\startx{6}
        
        % Создаем 3 последовательных прямоугольных области
        % Прямоугольник 0 (синий) - от 5.85 до 6.15, высота f(6) = 0.192
        \fill[blue!60, fill opacity=0.8] (5.85,0) rectangle (6.15,0.192);
        \draw[thick, blue!80!black] (5.85,0) -- (5.85,0.192);
        \draw[thick, blue!80!black] (6.15,0) -- (6.15,0.192);
        \draw[thick, blue!80!black] (5.85,0.192) -- (6.15,0.192);
        \draw[thick, blue!80!black] (6,0) -- (6,-0.02);
        
        % Прямоугольник 1 (зеленый) - от 6.15 до 6.45, высота f(6.3) = 0.166
        \fill[green!60, fill opacity=0.8] (6.15,0) rectangle (6.45,0.185);
        \draw[thick, green!80!black] (6.15,0) -- (6.15,0.185);
        \draw[thick, green!80!black] (6.45,0) -- (6.45,0.185);
        \draw[thick, green!80!black] (6.15,0.185) -- (6.45,0.185);
        \draw[thick, green!80!black] (6.3,0) -- (6.3,-0.02);
        
        % Прямоугольник 2 (красный) - от 6.45 до 6.75, высота f(6.6) = 0.128
        \fill[red!60, fill opacity=0.8] (6.45,0) rectangle (6.75,0.178);
        \draw[thick, red!80!black] (6.45,0) -- (6.45,0.178);
        \draw[thick, red!80!black] (6.75,0) -- (6.75,0.178);
        \draw[thick, red!80!black] (6.45,0.178) -- (6.75,0.178);
        \draw[thick, red!80!black] (6.6,0) -- (6.6,-0.02);        
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.5cm]
        % Объединенная формула для массы
        \node[draw, fill=gray!10, rounded corners, minimum width=6.2cm, minimum height=1.5cm] at (0.5,1.3) {
            \begin{minipage}{6.2cm}
                \centering
                $P(a < X < b) = \sum f_X(x_i) dx = \int\limits_{a}^{b}f_X(x)dx$ \\
            \end{minipage}
        };
                
        % Стрелка к зеленой области в первом графике
        \draw[thick, green!80!black, ->] (-2.,1.1) -- (-5.9,1.0);
        
        % Стрелка к зеленой области во втором графике (x_0 = 7)
        \draw[thick, green!80!black, ->] (-2.,1.1) -- (-4.7,-1.0);
    \end{scope}
    
\end{tikzpicture}

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

## Нормальное распределение

\begin{itemize}
    \item Функция плотности вероятности параметризована двумя константами $\mu$ и $\sigma^2$ и записывается как:
$$
    f_X(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}, \; \forall x \in \mathbb{R}
$$

    \item Параметры влияют на вид функции плотности и, как следствие, на "поведение" нормальной случайной величины. Чтобы подчеркнуть конкретную нормальную величину, с конкретно рассматриваемым набором параметров, мы пишем:
$$
    X \sim \mathcal{N} \, (\mu, \sigma^2)
$$

\end{itemize}

::: {.callout-note title="Характеристики нормальной величины"}
Имеет место интересное совпадение параметров и характеристик нормальной случайной величины:
$$
    E[X] = \mu, \; Var[X] = \sigma^2
$$
Будьте внимательны, в общем случае параметры и характеристики случайной величины совпадать не обязаны.
:::

## Влияние параметров на функцию плотности

![Влияние параметра $\mu$](mu_influence_normal.pdf){#fig-mu}

## Влияние параметров на функцию плотности

![Влияние параметра $\sigma$](sigma_influence_normal.pdf){#fig-sigma}

## Влияние параметров на функцию плотности

![Влияние параметра $\sigma$](sigma_area_diff.pdf){#fig-sigma-diff}

## Стандартная нормальная величина
### Все нормальные равны, но одно равнее других

\begin{itemize}
    \item Поскольку существует бесконечное число пар $(\mu, \sigma^2)$, существует также бесконечное число различных нормальных распределений.
    \item Это потребовало бы вычисления десятков сложных вероятностных интегралов каждый раз.
    \item Что если вычисление вероятности \textbf{любой} нормальной СВ можно свести к знанию всего одной переменной?
\end{itemize}

## Стандартная нормальная величина
### Все нормальные равны, но одно равнее других

\begin{itemize}
    \item Встречайте \textit{стандартную} нормальную случайную величину:
$$
    Z \sim \mathcal{N} \, (0,1), \quad f_Z(x) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^2}{2}}, \; \forall x \in \mathbb{R}
$$

    \item Давным-давно математики вычислили десятки вероятностных интегралов и создали таблицу стандартного нормального распределения, которая показывает значения функции распределения $F_Z(x)$ для многих возможных значений $x$.
    \item Мы можем найти любую вероятность любой нормальной случайной величины, преобразовав её в стандартную нормальную.
\end{itemize}

## Стандартная нормальная величина
### Формула преобразования

- Пусть $X$ — нормальная случайная величина и $X \sim \mathcal{N} \, (\mu, \sigma^2)$.
- Тогда следующая функция (преобразование) преобразует $X$ в стандартную нормальную величину:
$$
    Z = \frac{X - \mu}{\sigma}
$$
![Преобразование в стандартную нормальную](x2z_transform.pdf){#fig-x2z}

## Стандартная нормальная величина

- Пусть $X$ — нормальная случайная величина и $X \sim \mathcal{N} \, (\mu, \sigma^2)$.
- Нас интересует некоторая вероятность $P(a < X < b)$, $\forall a, \, b: a \leq b$.
- Применим преобразование к каждой части неравенства, чтобы не нарушить его:
\begin{equation*}
    P(a < X < b) = P \left( \underbrace{\frac{a - \mu}{\sigma}}_{\tilde{a}} < \underbrace{\frac{X - \mu}{\sigma}}_{Z} < \underbrace{\frac{b - \mu}{\sigma}}_{\tilde{b}}  \right) =  P \left( \tilde{a} < Z < \tilde{b} \right) = F_Z(\tilde{b}) - F_Z(\tilde{a}).
\end{equation*}

## Стандартная нормальная величина

![Вычисление вероятности с использованием ФР](normal_cdf_diff.pdf){#fig-normal_cdf_diff}

## Стандартная нормальная величина
![Таблица стандартного нормального распределения](normal_distr_table.pdf){#fig-normal_table}


## Пример

Если $X$ — нормально распределенная случайная величина со средним $6$ и дисперсией $25$, найти:
    \begin{enumerate}
        \item $P(6 \leq X \leq 12)$,
        \item $P(0 \leq X \leq 8)$,
        \item $P(-2 < X \leq 0)$.
    \end{enumerate}

## Пример
### Вопрос 1

$P(6 \leq X \leq 12)$

\begin{itemize}
    \item $X \sim \mathcal{N}(6, 25)$, значит $\mu = 6$, $\sigma = 5$
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(6 \leq X \leq 12) = P\left(\frac{6-6}{5} \leq Z \leq \frac{12-6}{5}\right) = P(0 \leq Z \leq 1.2)$
    \item $= F_Z(1.2) - F_Z(0) = 0.8849 - 0.5 = 0.3849$
\end{itemize}

## Пример
### Визуализация вопроса 1

![](problem_1.png){#fig-problem-1 width=70%}

## Пример
### Вопрос 2

$P(0 \leq X \leq 8)$

\begin{itemize}
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(0 \leq X \leq 8) = P\left(\frac{0-6}{5} \leq Z \leq \frac{8-6}{5}\right) = P(-1.2 \leq Z \leq 0.4)$
    \item Используем свойство симметрии: $F_Z(-1.2) = 1 - F_Z(1.2) = 1 - 0.8849 = 0.1151$
    \item $= F_Z(0.4) - F_Z(-1.2) = 0.6554 - 0.1151 = 0.5403$
\end{itemize}

## Пример
### Визуализация вопроса 2

![Визуализация вопроса 2](problem_2.png){#fig-problem-2 width=70%}

## Пример
### Вопрос 3

$P(-2 < X \leq 0)$

\begin{itemize}
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(-2 < X \leq 0) = P\left(\frac{-2-6}{5} < Z \leq \frac{0-6}{5}\right) = P(-1.6 < Z \leq -1.2)$
    \item Используем свойство симметрии: $F_Z(-1.2) = 1 - F_Z(1.2) = 1 - 0.8849 = 0.1151$
    \item $F_Z(-1.6) = 1 - F_Z(1.6) = 1 - 0.9452 = 0.0548$
    \item $= F_Z(-1.2) - F_Z(-1.6) = 0.1151 - 0.0548 = 0.0603$
\end{itemize}

## Пример
### Визуализация вопроса 3

![Визуализация вопроса 3](problem_3.png){#fig-problem-3 width=70%}

## Многомерное нормальное распределение

:::{.callout-definition}
Пара случайных величин $(X, Y)$ имеет **двумерное нормальное распределение**, если для всех $a, b \in \mathbb{R}$ линейная комбинация $aX + bY$ имеет одномерное нормальное распределение.
:::

:::{.callout-definition}
Вектор случайных величин $\mathbf{X} = (X_1, X_2, \ldots, X_n)$ имеет **многомерное нормальное распределение**, если для всех векторов $\mathbf{a} \in \mathbb{R}^n$ линейная комбинация $\mathbf{a}^{\top} \mathbf{X}$ имеет одномерное нормальное распределение.

$\mathbf{a}^{\top} \mathbf{X} = a_1 X_1 + a_2 X_2 + \ldots + a_n X_n$
:::


## Устойчивость нормального распределения

\begin{itemize}
    \item \textbf{Ключевое свойство}: Нормальное распределение \textbf{устойчиво} относительно линейных преобразований.
    
    \item Если $X \sim \mathcal{N}(\mu, \sigma^2)$, то для любых констант $a \neq 0$ и $b$:
    $$
    Y = aX + b \sim \mathcal{N}(a\mu + b, a^2\sigma^2)
    $$
    
    \item \textbf{Интерпретация}: Линейное преобразование нормальной случайной величины даёт нормальную случайную величину.
\end{itemize}

## Устойчивость нормального распределения
### Линейная комбинация двух независимых нормальных величин

\begin{itemize}
    \item Частный случай: если $X_1 \sim \mathcal{N}(\mu_1, \sigma_1^2)$ и $X_2 \sim \mathcal{N}(\mu_2, \sigma_2^2)$ независимы, то:
    $$
    X_1 + X_2 \sim \mathcal{N}(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)
    $$
    
    \item \textbf{Связь с многомерным нормальным}: Независимые нормальные величины $(X_1, X_2)$ формируют двумерное нормальное распределение, поэтому любая линейная комбинация $aX_1 + bX_2$ имеет нормальное распределение.
\end{itemize}

## Устойчивость нормального распределения
### Обобщение на $n$ переменных

\begin{itemize}
    \item Пусть $X_1, \ldots, X_n$ — независимые нормальные случайные величины:
    $$
    X_i \sim \mathcal{N}(\mu_i, \sigma_i^2), \quad i = 1, \ldots, n
    $$
    
    \item \textbf{Важно}: Вектор (коллекция, набор) независимых нормальных случайных величин имеет \textbf{многомерное нормальное распределение}.
    
    \item По определению многомерного нормального распределения, \textbf{любая} линейная комбинация имеет нормальное распределение:
    $$
    Y = \sum_{i=1}^{n} a_i X_i \sim \mathcal{N}\left(\sum_{i=1}^{n} a_i \mu_i, \sum_{i=1}^{n} a_i^2 \sigma_i^2\right)
    $$
\end{itemize}
