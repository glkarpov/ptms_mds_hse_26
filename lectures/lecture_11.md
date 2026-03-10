---
title: "Теория вероятностей и математическая статистика"
subtitle: "Непрерывные случайные величины."
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

## Мотивация для нового класса случайных величин

::: {.columns}
::: {.column width="50%"}
\textbf{Пример 1: Физические измерения}
\begin{itemize}
\item Рост человека
\item Температура воздуха
\item Скорость автомобиля
\end{itemize}

\textbf{Пример 2: Время ожидания}
\begin{itemize}
\item Время "жизни" детали
\item Время между звонками в call-центр
\end{itemize}
:::

::: {.column width="50%"}
\textbf{Пример 3: Экономические показатели}
\begin{itemize}
\item Доходы компании
\item Цены на акции
\end{itemize}

\textbf{Пример 4: Технические параметры}
\begin{itemize}
\item Напряжение в сети
\item Давление в шинах
\item Концентрация вещества
\end{itemize}
:::
:::

### Почему дискретные СВ не подходят?

\begin{itemize}
\item \textbf{Бесконечное количество значений}: Время может быть 1.234567 секунды
\item \textbf{Непрерывность}: Между любыми двумя значениями есть промежуточные
\item \textbf{Точность измерений}: Современные приборы дают очень точные результаты
\end{itemize}

### Вероятность в точке теряет смысл

\begin{itemize}
\item Для непрерывных величин вероятность \textbf{точечного} события P(X = a) всегда равна нулю
\item Отныне нас будует интересовать только вероятности попадания в \textbf{интервалы}:
$$
    P(a < X < b), \; P(X > c), \; P(X < d)
$$
\end{itemize}

## Физическое \cancel{Лирическое} вступление
- Вспомним физику 8-го класса и формулу
$$
    m = \rho \cdot V, \quad [kg] = \left[\frac{kg}{m^3}\right] [m^3]
$$

- Можем перейти к *линейной* или *погонной* плотности $\rho_l = \left[\frac{kg}{m}\right]$, которая покажет нам массу единицы длины некого объекта (метр проволоки, метр провода, метр плитки шоколада). Тогда масса объекта длины $L$ будет:
$$
    m = \rho_l \cdot L
$$

## Связь линейной плотности и массы

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
            ytick={0,1},
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
        
        % Рисуем функцию плотности
        \addplot[thick, red, domain=0:10, samples=100] {0.1};
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);        
        \end{axis}
    \end{scope}

    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=11cm, yshift=0.0cm]
        % Кусочно-заданная функция
        \node[draw, fill=gray!10, rounded corners, minimum width=3.5cm, minimum height=2cm] at (0.5, 1.0) {
            \begin{minipage}{3.4cm}
                \centering
                $\rho(x) = \begin{cases}
                0, & x < 0 \\
                0.1, & 0 \leq x \leq 10 \\
                0, & x > 10
                \end{cases}$
            \end{minipage}
        };
    \end{scope}
\end{tikzpicture}

## Связь линейной плотности и массы

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
            ytick={0,1},
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
        
        % Заливаем область под графиком плотности
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=100] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.5cm]
        % Объединенная формула для массы
        \node[draw, fill=gray!10, rounded corners, minimum width=3.5cm, minimum height=1.5cm] at (0.5,1.3) {
            \begin{minipage}{3.3cm}
                \centering
                $m = \rho_l \cdot L$\\
                \small Масса = площадь под графиком плотности
            \end{minipage}
        };
        
        % Стрелка к металлической пластине
        \draw[thick, blue, ->] (0.25,1.4) -- (-3.1,2.8);
        \node[blue, left] at (-1.8,1.5) {$\rho_l = \frac{1}{10}$};
        
        % Стрелка к области под графиком плотности
        \draw[thick, red, ->] (0.25,1.4) -- (-3.7,1.0);
        \node[red, left] at (-1.8,-0.5) {Площадь = $\frac{1}{10} \cdot 10 = 1$};
    \end{scope}
    
\end{tikzpicture}

## Связь линейной плотности и массы
### Значение плотности в точке

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
            ytick={0,1},
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


## Связь линейной плотности и массы
### Переменная плотность

- Не всегда линейная плотность является постоянной! В нашей аналогии из физики мы можем себе представить рельс, у которого единица длины плавно становится тяжелее от краев к центру.

\begin{tikzpicture}
    % Верхний график - Рельс :)
    \begin{scope}[yshift=2cm]
        \begin{axis}[
            width=10cm,
            height=2cm,
            xmin=-1, xmax=12,
            ymin=-0.5, ymax=1.5,
            axis lines=center,
            xlabel={$x$},
            ylabel={Объект},
            xtick={0,2,4,6,8,10},
            ytick={0,1},
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
        
        % Добавляем текстовую метку
        \node[above] at (5,1) {Рельс из платиново-пластикового сплава :)};
        
        \end{axis}
    \end{scope}
    
    % Нижний график - переменная плотность
    \begin{scope}[yshift=-1cm]
        \begin{axis}[
            width=10cm,
            height=4cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=0.25,
            axis lines=center,
            xlabel={$x$},
            ylabel={Плотность $\rho(x)$},
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
        
        % Заливаем область под графиком переменной плотности
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=100] {0.2 * (1 - (x-5)^2/25)} \closedcycle;
        
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.5cm]
        % Объединенная формула для массы
        \node[draw, fill=gray!10, rounded corners, minimum width=3.5cm, minimum height=1.5cm] at (0.5,0.3) {
            \begin{minipage}{3.3cm}
                \centering
                $m = \int_0^{10} \rho(x) dx$\\
                \small Масса = площадь под графиком плотности
            \end{minipage}
        };
        
        % Стрелка к металлической пластине
        \draw[thick, blue, ->] (-0.5,0.5) -- (-3.1,1.8);

        % Стрелка к области под графиком плотности
        \draw[thick, red, ->] (-0.5,0.5) -- (-3.7,0.0);
        \node[red, left] at (-1.8,-0.5) {Площадь = $\int_0^{10} \rho(x) dx$};
    \end{scope}
    
\end{tikzpicture}

## Кумулятивная масса

- Теперь мы хотим ввести функцию, которая покажет нам, сколько массы "скопилось" к координате $x$.

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
            ytick={0,1},
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
        
        % Заливаем область под графиком плотности
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=100] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        \end{axis}
    \end{scope}
    
    % Третий график - кумулятивная масса
    \begin{scope}[yshift=-2.0cm]
        \begin{axis}[
            width=10cm,
            height=3cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=1.2,
            axis lines=center,
            xlabel={$x$},
            ylabel={Кумулятивная масса $M(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.5,1},
            yticklabels={0,0.5,1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем кумулятивную массу
        \addplot[thick, violet, domain=-1:0, samples=10] {0};
        \addplot[thick, violet, domain=0:10, samples=100] {0.1*x};
        \addplot[thick, violet, domain=10:12, samples=10] {1};      
        \end{axis}
    \end{scope}
    
    % Добавляем формулу и стрелки справа
    \begin{scope}[xshift=10cm, yshift=0.0cm]
        % Формула для кумулятивной массы
        \node[draw, fill=violet!10, rounded corners, minimum width=3.5cm, minimum height=1.5cm] at (0.5,0.5) {
            \begin{minipage}{3.3cm}
                \centering
                $M(x) = \int_0^x \rho(t) dt$\\
                \small Кумулятивная масса
            \end{minipage}
        };
        
        % Кусочно-заданная функция
        \node[draw, fill=gray!10, rounded corners, minimum width=3.5cm, minimum height=2cm] at (0.5,-1.5) {
            \begin{minipage}{3.3cm}
                \centering
                $M(x) = \begin{cases}
                0, & x < 0 \\
                0.1x, & 0 \leq x \leq 10 \\
                1, & x > 10
                \end{cases}$
            \end{minipage}
        };
        
        % Стрелка к кумулятивной массе
        \draw[thick, violet, ->] (0.25,0.5) -- (-3.7,-0.5);
        \node[violet, left] at (-1.8,0) {Кумулятивная масса};
    \end{scope}
    
\end{tikzpicture}

## Кумулятивная масса
### Пример 1

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
            ytick={0,1},
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
        
        % Зеленая область на металлической пластине (смешивание с синим)
        \addplot[thick, green!80!blue, fill=green!60!blue!40, fill opacity=0.8, domain=0:2, samples=100] {0.1} \closedcycle;
        \addplot[thick, green!80!blue, fill=green!60!blue!40, fill opacity=0.8, domain=0:2, samples=100] {0.9} \closedcycle;
        
        % Вертикальные линии для области от 0 до 2
        \draw[thick, green!80!blue] (0,0.1) -- (0,0.9);
        \draw[thick, green!80!blue] (2,0.1) -- (2,0.9);
        
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
        
        % Заливаем область под графиком плотности
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=100] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        % Вертикальная пунктирная линия от точки x=2
        \draw[green, thick, dashed] (2,0) -- (2,0.1);
        
        % Заливаем область от 0 до x=2
        \addplot[thick, green, fill=green!30, fill opacity=0.7, domain=0:2, samples=100] {0.1} \closedcycle;
        
        \end{axis}
    \end{scope}
    
    % Третий график - кумулятивная масса
    \begin{scope}[yshift=-2.0cm]
        \begin{axis}[
            width=10cm,
            height=3cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=1.2,
            axis lines=center,
            xlabel={$x$},
            ylabel={Кумулятивная масса $M(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.5,1},
            yticklabels={0,0.5,1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем кумулятивную массу
        \addplot[thick, violet, domain=-1:0, samples=10] {0};
        \addplot[thick, violet, domain=0:10, samples=100] {0.1*x};
        \addplot[thick, violet, domain=10:12, samples=10] {1};
        
        % Добавляем зеленую точку на кумулятивной массе
        \addplot[mark=*, mark size=4pt, green] coordinates {(2, 0.2)};
        
        % Добавляем подпись к точке
        \node[green, right] at (2.1, 0.2) {$M(2) = 0.2$};
        
        \end{axis}
    \end{scope}    
\end{tikzpicture}

## Кумулятивная масса
### Пример 2

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
            ytick={0,1},
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
        
        % Оранжевая область на металлической пластине (смешивание с синим)
        \addplot[thick, orange!80!blue, fill=orange!60!blue!40, fill opacity=0.8, domain=0:4, samples=100] {0.1} \closedcycle;
        \addplot[thick, orange!80!blue, fill=orange!60!blue!40, fill opacity=0.8, domain=0:4, samples=100] {0.9} \closedcycle;
        
        % Вертикальные линии для области от 0 до 4
        \draw[thick, orange!80!blue] (0,0.1) -- (0,0.9);
        \draw[thick, orange!80!blue] (4,0.1) -- (4,0.9);
        
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
        
        % Заливаем область под графиком плотности
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=100] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=10] {0};
        \addplot[thick, red, domain=10:12, samples=10] {0};
        
        % Добавляем вертикальные линии на границах
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        
        % Вертикальная пунктирная линия от точки x=4
        \draw[orange, thick, dashed] (4,0) -- (4,0.1);
        
        % Заливаем область от 0 до x=4
        \addplot[thick, orange, fill=orange!30, fill opacity=0.7, domain=0:4, samples=100] {0.1} \closedcycle;
        
        \end{axis}
    \end{scope}
    
    % Третий график - кумулятивная масса
    \begin{scope}[yshift=-2.0cm]
        \begin{axis}[
            width=10cm,
            height=3cm,
            xmin=-1, xmax=12,
            ymin=-0.1, ymax=1.2,
            axis lines=center,
            xlabel={$x$},
            ylabel={Кумулятивная масса $M(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.5,1},
            yticklabels={0,0.5,1},
            xlabel style={below},
            ylabel style={left},
            grid=major,
            grid style={dashed,gray!30},
            clip=false
        ]
        
        % Рисуем кумулятивную массу
        \addplot[thick, violet, domain=-1:0, samples=10] {0};
        \addplot[thick, violet, domain=0:10, samples=100] {0.1*x};
        \addplot[thick, violet, domain=10:12, samples=10] {1};
        
        % Добавляем оранжевую точку на кумулятивной массе
        \addplot[mark=*, mark size=4pt, orange] coordinates {(4, 0.4)};
        
        % Добавляем подпись к точке
        \node[orange, right] at (4.1, 0.4) {$M(4) = 0.4$};
        
        \end{axis}
    \end{scope}    
\end{tikzpicture}


## Функция плотности вероятности

- :::{.callout-definition}
Мы называем $X$ непрерывной случайной величиной, если существует неотрицательная функция $f_X(x)$, определенная для $\forall x \in \mathbb{R}$, такая что любая вероятность вида $P(a \leq X \leq b)$ может быть найдена по формуле:
$$
   P(a \leq X \leq b) = \int \limits_{a}^{b} f_X(x) dx  
$$
:::

- Нормировка вероятности. Поскольку $P(\Omega_X)$ должно быть равно $1$, здесь мы имеем:
$$ 
    1 = P(\Omega_X) = P \{ X \in (-\infty, +\infty) \} = \int \limits_{-\infty}^{+\infty} f_X(x) dx
$$

## Функция плотности вероятности
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

## Функция плотности вероятности
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

## Функция распределения (кумулятивная / интегральная)

- :::{.callout-definition}
Кумулятивная функция распределения случайной величины $X$ - это неубывающая функция $F_X(x)$, определенная для $\forall x \in \mathbb{R}$, такая что:

$$
    F_X(x) = P \{ X \in (-\infty, x] \} = P \{ X \leq x \}
$$

- Для непрерывной случайной величины мы можем переписать это как:
$$
    F_X(x) = P \{ X \in (-\infty, x] \} = \int \limits_{-\infty}^{x} f_X(t) dt
$$

- Основные свойства:
$$
    F_X(-\infty) = 0, \quad \quad F_X(\infty) = 1
$$


## Функция распределения как способ избежать интегрирования

- Предположим, нас интересует $P(a < X < b)$. Рассмотрим интервал $\mathcal{D} = (-\infty, b)$. Его можно разложить на объединение двух непересекающихся множеств: $\mathcal{D} = (-\infty, \; a] \cup (a, \; b)$.

- Согласно принципу аддитивности вероятности:
$$
    P\{ X \in \mathcal{D} \} = P\{ X \in (-\infty, \; a] \} + P \{ X \in (a, \; b) \}
$$

- В интегральной формулировке:
$$
    \int \limits_{-\infty}^{b} f_X(x) dx = \int \limits_{-\infty}^{a} f_X(x) dx  + \int \limits_{a}^{b} f_X(x) dx
$$

- Наконец:
$$
    \boxed{\int \limits_{a}^{b} f_X(x) dx = F_X(b) - F_X(a)} 
$$
Функция плотности вероятности является производной от функции распределения:
$$
    f_X(x) = F_X'(x) = \frac{d}{dx} F_X(x)
$$

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
    \int\limits_{-\infty}^{x}f_X(t)dt = \int\limits_{-\infty}^{0}\textcolor{red}{f_X(t)}dt + \int\limits_{0}^{3}\textcolor{violet}{f_X(t)}dt + \int\limits_{3}^{+\infty} \textcolor{blue}{f_X(t)} dt =
     \int\limits_{-\infty}^{0}\textcolor{red}{0} \, dt + \int\limits_{0}^{3}\textcolor{violet}{\frac{1 t^2}{9}}dt + \int\limits_{3}^{+\infty}\textcolor{blue}{0} \, dt = 1
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
