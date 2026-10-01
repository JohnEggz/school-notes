# Teoria sygnalów wykład 1

## Wykład zadanie 1. Animacja Koło
```matlab
%% Metryczka
% Program do testu wykresów matlab
% Grzegorz Patro
% 01-10-2026

%% Porządki wstępne
clear;
close all;
clc;

function a = my_anim(my_step)
    %% Część obliczeniowa
    % Parametry sygnału
    f0 = 1;
    phi0 = pi/3;
    t = linspace(-2, 2, 200);
    x = cos(2 * pi * f0 * t + phi0);
    y = sin(2 * pi * f0 * t + phi0);
    
    % Punkty pomiarowe / śledzone
    t_pts = [0, 0.2];
    t_pts = t_pts + my_step;
    x_pts = cos(2 * pi * f0 * t_pts + phi0);
    y_pts = sin(2 * pi * f0 * t_pts + phi0);
    
    %% Wykres 1: Sygnał w dziedzinie czasu x(t)
    figure(1);
    subplot(1,2,1);
    plot(t, x, 'r.-');
    hold on;
    plot(t_pts, x_pts, 'co', ...
        'MarkerSize', 8, ...
        'MarkerFaceColor', 'c', ...
        'MarkerEdgeColor', 'b');
    
    % pogrubiona linia osi
    yline(0, 'w-', 'LineWidth', 2);
    xline(0, 'w-', 'LineWidth', 2);
    hold off;
    
    grid on;
    axis equal;
    xlabel('t [s]');
    ylabel('x(t)');
    title('Wykres x(t)');
    
    %% Wykres 2: Wykres fazorowy / parametryczny y(x)
    subplot(1,2,2);
    plot(x, y, 'r.-');
    hold on;
    plot(x_pts, y_pts, 'co', ...
        'MarkerSize', 8, ...
        'MarkerFaceColor', 'c', ...
        'MarkerEdgeColor', 'b');
    plot([0, x_pts(1)], [0, y_pts(1)], 'b-', 'LineWidth', 2);
    yline(0, 'w-', 'LineWidth', 2);
    xline(0, 'w-', 'LineWidth', 2);
    hold off;

    grid on;
    axis equal;
    xlabel('x(t)');
    ylabel('y(t)');
    title('Wykres parametryczny y(x)');
end

for myStep = linspace(-2, 2, 100)
    my_anim(myStep);
    pause(0.5);
end

```

## Wykład 1 zadanie 2. Prawdziwy Cosinus

```matlab
%% Metryczka
% Prawdziwy cosinus (impuls prostokątny i sygnał okienkowany)
% Grzegorz Patro
% 01-10-2026

%% Porządki wstępne
clear;
close all;
clc;

%% Parametry i obliczenia
% Oś czasu
t = linspace(-2, 2, 1000);

% Parametry fali nośnej
f0 = 2;
phi0 = 0;

% Sygnały
y1 = Pi(t);
y2 = cos(2 * pi * f0 * t + phi0);
y3 = y1 .* y2;

%% Wizualizacja
figure(1);

% 1. Impuls prostokątny Pi(t)
subplot(1, 3, 1);
plot(t, y1, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
xlabel('t [s]');
ylabel('y_1(t)');

% 2. Kosinusoida ciągła
subplot(1, 3, 2);
plot(t, y2, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
xlabel('t [s]');
ylabel('y_2(t)');

% 3. Sygnał wypadkowy
subplot(1, 3, 3);
plot(t, y3, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
xlabel('t [s]');
ylabel('y_3(t)');

%% Funkcje lokalne
function y = Pi(t)
    y = zeros(size(t));
    abs_t = abs(t);

    y(abs_t < 0.5) = 1;
    y(abs_t == 0.5) = 0.5;
end
```

## Wykład 1 Zadanie 3. Operacje na sygnałach

```matlab
%% Metryczka
% Operacje na sygnalach
% Grzegorz Patro
% 01-10-2026

%% Porządki wstępne
clear;
close all;
clc;

%% Parametry i obliczenia
% Oś czasu
t = linspace(-4, 4, 1000);

% Sygnały
x1 = 0.5 * Pi(t/2);
x2 = -1 * Pi((t+1.5)/3);
x3 = x1 + x2;

%% Wizualizacja
figure(1);

% 1. Impuls prostokątny Pi(t)
subplot(3, 1, 1);
plot(t, x1, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
ylim([-1.2, 1.2])
xlabel('t [s]');
ylabel('y_1(t)');

% 2. Kosinusoida ciągła
subplot(3, 1, 2);
plot(t, x2, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
ylim([-1.2, 1.2])
xlabel('t [s]');
ylabel('y_2(t)');

% 3. Sygnał wypadkowy
subplot(3, 1, 3);
plot(t, x3, 'r-', 'LineWidth', 1.5);
grid on;
axis padded;
ylim([-1.2, 1.2])
xlabel('t [s]');
ylabel('y_3(t)');

%% Funkcje lokalne
function y = Pi(t)
y = zeros(size(t));
abs_t = abs(t);

y(abs_t < 0.5) = 1;
y(abs_t == 0.5) = 0.5;
end
```