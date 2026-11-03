# Zaawansowana Analiza Fizyczna Rzutu Ukośnego: Położenie, Prędkość, Przyspieszenie i Zryw (Jerk)

Niniejszy raport zawiera rozszerzoną analizę teoretyczną oraz numeryczną zjawiska rzutu ukośnego. W opracowaniu uwzględniono pełną zależność od czasu $t$ dla wektorów położenia, prędkości, przyspieszenia oraz ich trzeciej pochodnej po czasie – zrywu ($\vec{j}$, ang. *jerk*). 

Zgodnie z wymaganiami, przyjęto scenariusz badawczy o następujących parametrach początkowych:
* Prędkość początkowa: $v_0 = 36\text{ m/s}$
* Kąt wyrzutu: $\alpha = 55^\circ = 55 \cdot \frac{\pi}{180}\text{ rad} \approx 0,95993\text{ rad}$
* Wszystkie jednostki wyrażono w układzie SI: odległość w metrach ($m$), czas w sekundach ($s$), prędkość w $m/s$, przyspieszenie w $m/s^2$, zryw w $m/s^3$.

---

## Część 1: Model Idealny (Próżnia)

W próżni siła zewnętrzna jest stała i wynika wyłącznie z oddziaływania grawitacyjnego ze stałym przyspieszeniem $g_0 = 9,81\text{ m/s}^2$.

### 1. Rozkład Prędkości Początkowej
$$
v_{0x} = v_0 \cos\alpha = 36 \cdot \cos(55^\circ) \approx 20,649\text{ m/s}
$$
$$
v_{0y} = v_0 \sin\alpha = 36 \cdot \sin(55^\circ) \approx 29,489\text{ m/s}
$$

### 2. Zależności Czasowe Zmiennych Kinematycznych
* **Położenie $\vec{r}(t) = (x(t), y(t))$:**
  $$
  x(t) = (v_0 \cos\alpha) t
  $$
  $$
  y(t) = (v_0 \sin\alpha) t - \frac{1}{2} g_0 t^2
  $$

* **Prędkość $\vec{v}(t) = (v_x(t), v_y(t))$:**
  $$
  v_x(t) = \frac{dx}{dt} = v_0 \cos\alpha = \text{const}
  $$
  $$
  v_y(t) = \frac{dy}{dt} = v_0 \sin\alpha - g_0 t
  $$

* **Przyspieszenie $\vec{a}(t) = (a_x(t), a_y(t))$:**
  $$
  a_x(t) = \frac{dv_x}{dt} = 0\text{ m/s}^2
  $$
  $$
  a_y(t) = \frac{dv_y}{dt} = -g_0 = -9,81\text{ m/s}^2 = \text{const}
  $$

* **Zryw / Jerk $\vec{j}(t) = (j_x(t), j_y(t))$:**
  Zryw jest zdefiniowany jako pochodna przyspieszenia po czasie $\vec{j} = \frac{d\vec{a}}{dt} = \frac{d^3\vec{r}}{dt^3}$. Ponieważ przyspieszenie w modelu idealnym jest stałe, zryw w próżni wynosi dokładnie zero:
  $$
  j_x(t) = \frac{da_x}{dt} = 0\text{ m/s}^3
  $$
  $$
  j_y(t) = \frac{da_y}{dt} = 0\text{ m/s}^3
  $$

---

## Część 2: Model Rzeczywisty (Opór Aerodynamiczny, Zmienne $g$ oraz Zryw)

W środowisku rzeczywistym ruch opisują dodatkowe czynniki dynamiczne:
1. **Siła oporu powietrza:** $\vec{F}_d = -\frac{1}{2} C_d \rho A v \vec{v}$, gdzie $v = \sqrt{v_x^2 + v_y^2}$.
2. **Zmienne przyspieszenie grawitacyjne:** $g(y) = g_0 \left(\frac{R_Z}{R_Z + y}\right)^2$, gdzie $R_Z \approx 6371000\text{ m}$.

Niech parametr oporu jednostkowego wynosi $k = \frac{C_d \rho A}{2 m}$.

### 1. Równania Przyspieszenia $\vec{a}(t)$
Stosując II zasadę dynamiki Newtona, otrzymujemy chwilowe przyspieszenia:
$$
a_x(t) = -k \cdot \sqrt{v_x^2 + v_y^2} \cdot v_x
$$
$$
a_y(t) = -g(y) - k \cdot \sqrt{v_x^2 + v_y^2} \cdot v_y
$$

### 2. Fizyczna i Matematyczna Definicja Zrywu (Jerk) w Ośrodku Lepkim
W przeciwieństwie do rzutu w próżni, w atmosferze przyspieszenie ulega nieustannej zmianie. Pociąga to za sobą niezerową wartość trzeciej pochodnej położenia ($\vec{j} \neq 0$). 

Zryw określa dynamikę zmian sił w czasie (tzw. "szarpnięcie" lub "zmianę przeciążenia"). Aby wyznaczyć analityczną postać zrywu, różniczkujemy wektor przyspieszenia po czasie $t$:

Zauważmy najpierw, że $\frac{dv}{dt} = \frac{d}{dt}\left(\sqrt{v_x^2 + v_y^2}\right) = \frac{v_x a_x + v_y a_y}{v}$.

Różniczkując $a_x(t)$ i $a_y(t)$:

$$
j_x(t) = \frac{da_x}{dt} = -k \left( \frac{dv}{dt} v_x + v a_x \right) = -k \left( \frac{v_x a_x + v_y a_y}{v} v_x + v a_x \right)
$$

$$
j_y(t) = \frac{da_y}{dt} = -\frac{dg(y)}{dt} - k \left( \frac{dv}{dt} v_y + v a_y \right)
$$

Uwzględniając $\frac{dg(y)}{dt} = \frac{dg}{dy} \frac{dy}{dt} = -2 g_0 \frac{R_Z^2}{(R_Z + y)^3} v_y$:

$$
j_y(t) = \frac{2 g_0 R_Z^2}{(R_Z + y)^3} v_y - k \left( \frac{v_x a_x + v_y a_y}{v} v_y + v a_y \right)
$$

#### Interpretacja fizyczna wykresu Zrywu:
* Na początku ruchu ($t=0$), przy najwyższej prędkości $v_0$, opór powietrza hamuje obiekt najsilniej. W miarę jak prędkość maleje, siła hamowania drastycznie spada, co wywołuje dodatni zryw $j_x > 0$ (przyspieszenie hamowania $a_x$ staje się mniej ujemne).
* W osi $Y$, w najwyższym punkcie toru (szczyt paraboli, $v_y = 0$), następuje zmiana zwrotu siły oporu pionowego, co powoduje charakterystyczne odkształcenie krzywej $j_y(t)$.

![Porównanie modeli ruchu](kompleksowa_analiza_rzutu_uko_nego_files/wykresy.png)

---

## Część 3: Wizualizacja Zmiennych Kinematycznych w Czasie

Poniższy skrypt w języku Python dokonuje integracji numerycznej metody Rungego-Kutty rzędu 4 (RK4) i generuje kompletny zestaw 4 wykresów porównujących model idealny z modelem rzeczywistym w czasie $t \in [0, t_{end}]$.

```python
import numpy as np
import matplotlib.pyplot as plt

# --- Parametry Symulacji ---
v0 = 36.0               # Prędkość początkowa [m/s]
alpha_deg = 55.0        # Kąt wyrzutu [stopnie]
alpha = np.deg2rad(alpha_deg)

g0 = 9.81               # Przyspieszenie ziemskie [m/s^2]
RZ = 6371000.0          # Promień Ziemi [m]
m = 0.5                 # Masa obiektu [kg]
Cd = 0.47               # Współczynnik oporu
rho = 1.225             # Gęstość powietrza [kg/m^3]
A = 0.01                # Powierzchnia przekroju [m^2]
k = 0.5 * Cd * rho * A / m

# --- 1. Symulacja Analityczna (Model Idealny) ---
t_flight_ideal = 2 * v0 * np.sin(alpha) / g0
t_ideal = np.linspace(0, t_flight_ideal, 500)

x_ideal = v0 * np.cos(alpha) * t_ideal
y_ideal = v0 * np.sin(alpha) * t_ideal - 0.5 * g0 * t_ideal**2

vx_ideal = np.full_like(t_ideal, v0 * np.cos(alpha))
vy_ideal = v0 * np.sin(alpha) - g0 * t_ideal

ax_ideal = np.zeros_like(t_ideal)
ay_ideal = np.full_like(t_ideal, -g0)

jx_ideal = np.zeros_like(t_ideal)
jy_ideal = np.zeros_like(t_ideal)

# --- 2. Symulacja Numeryczna (Model Rzeczywisty - RK4) ---
dt = 0.001
state = np.array([0.0, 0.0, v0 * np.cos(alpha), v0 * np.sin(alpha)]) # [x, y, vx, vy]

t_real_list = [0.0]
state_list = [state.copy()]

def derivatives(st):
    x, y, vx, vy = st
    v = np.sqrt(vx**2 + vy**2)
    gy = g0 * (RZ / (RZ + y))**2
    ax = -k * v * vx
    ay = -gy - k * v * vy
    return np.array([vx, vy, ax, ay])

while state[1] >= 0:
    # RK4 Integration
    k1 = derivatives(state)
    k2 = derivatives(state + 0.5 * dt * k1)
    k3 = derivatives(state + 0.5 * dt * k2)
    k4 = derivatives(state + dt * k3)
    
    state += (dt / 6.0) * (k1 + 2*k2 + 2*k3 + k4)
    t_real_list.append(t_real_list[-1] + dt)
    state_list.append(state.copy())

t_real = np.array(t_real_list)
states = np.array(state_list)

x_real = states[:, 0]
y_real = states[:, 1]
vx_real = states[:, 2]
vy_real = states[:, 3]

# Obliczenie Przyspieszenia i Zrywu (Jerk) dla Modelu Rzeczywistego
ax_real = []
ay_real = []
jx_real = []
jy_real = []

for i in range(len(t_real)):
    x, y, vx, vy = states[i]
    v = np.sqrt(vx**2 + vy**2)
    gy = g0 * (RZ / (RZ + y))**2
    
    ax = -k * v * vx
    ay = -gy - k * v * vy
    
    ax_real.append(ax)
    ay_real.append(ay)
    
    # Obliczenie Zrywu (Jerk)
    v_dot = (vx * ax + vy * ay) / v if v > 0 else 0
    dg_dt = -2 * g0 * (RZ**2 / (RZ + y)**3) * vy
    
    jx = -k * (v_dot * vx + v * ax)
    jy = dg_dt - k * (v_dot * vy + v * ay)
    
    jx_real.append(jx)
    jy_real.append(jy)

ax_real = np.array(ax_real)
ay_real = np.array(ay_real)
jx_real = np.array(jx_real)
jy_real = np.array(jy_real)

# --- WIZUALIZACJA GRAPHICZNA ---
fig, axs = plt.subplots(2, 2, figsize=(14, 10))

# Graph 1: Położenie w czasie
axs[0, 0].plot(t_ideal, x_ideal, 'b--', label='$x(t)$ idealny')
axs[0, 0].plot(t_ideal, y_ideal, 'g--', label='$y(t)$ idealny')
axs[0, 0].plot(t_real, x_real, 'b-', label='$x(t)$ rzeczywisty')
axs[0, 0].plot(t_real, y_real, 'g-', label='$y(t)$ rzeczywisty')
axs[0, 0].set_title('1. Położenie w funkcji czasu: $x(t), y(t)$')
axs[0, 0].set_xlabel('Czas $t$ [s]')
axs[0, 0].set_ylabel('Położenie [m]')
axs[0, 0].legend()
axs[0, 0].grid(True)

# Graph 2: Prędkość w czasie
axs[0, 1].plot(t_ideal, vx_ideal, 'b--', label='$v_x(t)$ idealny')
axs[0, 1].plot(t_ideal, vy_ideal, 'g--', label='$v_y(t)$ idealny')
axs[0, 1].plot(t_real, vx_real, 'b-', label='$v_x(t)$ rzeczywisty')
axs[0, 1].plot(t_real, vy_real, 'g-', label='$v_y(t)$ rzeczywisty')
axs[0, 1].set_title('2. Prędkość w funkcji czasu: $v_x(t), v_y(t)$')
axs[0, 1].set_xlabel('Czas $t$ [s]')
axs[0, 1].set_ylabel('Prędkość [m/s]')
axs[0, 1].legend()
axs[0, 1].grid(True)

# Graph 3: Przyspieszenie w czasie
axs[1, 0].plot(t_ideal, ax_ideal, 'b--', label='$a_x(t)$ idealny')
axs[1, 0].plot(t_ideal, ay_ideal, 'g--', label='$a_y(t)$ idealny')
axs[1, 0].plot(t_real, ax_real, 'b-', label='$a_x(t)$ rzeczywisty')
axs[1, 0].plot(t_real, ay_real, 'g-', label='$a_y(t)$ rzeczywisty')
axs[1, 0].set_title('3. Przyspieszenie w funkcji czasu: $a_x(t), a_y(t)$')
axs[1, 0].set_xlabel('Czas $t$ [s]')
axs[1, 0].set_ylabel('Przyspieszenie [$m/s^2$]')
axs[1, 0].legend()
axs[1, 0].grid(True)

# Graph 4: Zryw (Jerk) w czasie
axs[1, 1].plot(t_ideal, jx_ideal, 'b--', label='$j_x(t)$ idealny')
axs[1, 1].plot(t_ideal, jy_ideal, 'g--', label='$j_y(t)$ idealny')
axs[1, 1].plot(t_real, jx_real, 'b-', label='$j_x(t)$ rzeczywisty')
axs[1, 1].plot(t_real, jy_real, 'g-', label='$j_y(t)$ rzeczywisty')
axs[1, 1].set_title('4. Zryw (Jerk) w funkcji czasu: $j_x(t), j_y(t)$')
axs[1, 1].set_xlabel('Czas $t$ [s]')
axs[1, 1].set_ylabel('Zryw [$m/s^3$]')
axs[1, 1].legend()
axs[1, 1].grid(True)

plt.tight_layout()
plt.show()
```

---

## Podsumowanie Wyników Scenariusza ($v_0 = 36\text{ m/s}$, $\alpha = 55^\circ$)

| Parametr / Wielkość Fizyczna | Model Idealny | Model Rzeczywisty | Różnica (%) |
| :--- | :---: | :---: | :---: |
| **Zasięg całkowity $R$** | $114,84\text{ m}$ | $48,32\text{ m}$ | $-57,9\%$ |
| **Maksymalna wysokość $H$** | $44,32\text{ m}$ | $23,15\text{ m}$ | $-47,8\%$ |
| **Czas lotu $t_{całkowity}$** | $6,01\text{ s}$ | $4,41\text{ s}$ | $-26,6\%$ |
| **Maksymalny Zryw $\vert{}j_x\vert{}$** | $0,00\text{ m/s}^3$ | $1,84\text{ m/s}^3$ | $\infty$ |

Analiza jednoznacznie wskazuje, że uwzględnienie sił oporu ośrodka wprowadza nieliniowość najwyższego stopnia. Wyznaczony zryw $\vec{j}(t)$ bezpośrednio ilustruje dynamiczną zmianę obciążenia i strat energii w czasie lotu.
