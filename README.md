# Marcov-chains-forecasting
## Proposal
Статья: <https://drive.google.com/file/d/1IihRh4PD2O_FHIpuRq-6VIf-O1v0hB18/view?usp=sharing>

**Данные:** почасовые данные о валютной паре EUR\USD и данные о WIG-20( промежуток между наблюдениями 1 день)

**Методы:** делим временной ряд валют на $N_w$ окон, в каждом из которых $N_c$ наблюдений. В каждом окне находим минимальное и максимальное значение величины и делим окно на $N_b$ равных промежутков, определяем каждый из промежутков как состояние. Стратегия основана на оценке значения матрицы переходных вероятностей между состояниями на каждом шаге. $P_{i,j}$ - распределение вероятностей для $j = 1,2 ... N_{b}$. То есть, $P_{i,i-1}$ - вероятность находиться в состоянии $S_{i-1}|q(t+1)$, если в момент времени t процесс был в состоянии $S_{i}|q(t)$ 
* Если $P_{i,i-1}$ < $P_{i,i+1}$, открываем длинную позицию;
* Если $P_{i,i-1} > P_{i,i+1}$, открываем короткую позицию;
* Если $P_{i,i-1} = P_{i,i+1}$, ничего;

Критерием качества стратегии используем прибыль (для длинных и коротких позиций) и риск (взвешенный на основе Calmar Ratio).
 Базовый подход: не учитываем StopLoss и transactional costs 
 Следующий шаг: добавляем StopLoss 

Методы оптимизации параметров: $C= max (w_{p} Z(N_{b}, N_c , N_w) + w_c CR(N_b, N_c , N_w)$
Где $Z(N_b, N_c , N_w)$ and $CR(N_b, N_c, N_w)$ - кумулятивная прибыль и Calmar Ratio, которые мы считаем для различных комбинаций параметров ${N_b, N_c, N_w}$ .
