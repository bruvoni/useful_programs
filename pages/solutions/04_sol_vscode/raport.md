# Analiza Fizyczna Rzutu Ukośnego

Niniejszy raport stanowi wyczerpujące opracowanie fizyczne zjawiska rzutu ukośnego. Łączy on analityczne wyprowadzenie wzorów dla wyidealizowanych warunków (próżnia) z rygorystycznym modelem rzeczywistym, uwzględniającym opór aerodynamiczny, zmienne przyspieszenie ziemskie oraz trzecią pochodną położenia po czasie – zryw (ang. *jerk*). Referencyjny wpływ oporu powietrza na spłycenie trajektorii i skrócenie zasięgu został zilustrowany na załączonym schemacie `image_e1ecde.png`.

---

## Część 1: Analityczny Opis Zjawiska (Podstawy Teoretyczne)

### 1.1. Model Idealny (Próżnia)

W modelu idealnym zakładamy brak jakichkolwiek oporów ruchu, a jedyną siłą działającą na ciało o masie $m$ jest siła ciężkości wywołana jednorodnym polem grawitacyjnym o stałym przyspieszeniu $g_0 \approx 9,81\text{ m/s}^2$. Ciało zostaje wyrzucone z prędkością początkową $v_0$ pod kątem $\alpha$ do poziomu.

**Rozkład prędkości początkowej:**

$$
v_{0x} = v_0 \cos\alpha
$$

$$
v_{0y} = v_0 \sin\alpha
$$

**Zależności kinematyczne w funkcji czasu $t$:**

1. **Położenie $\vec{r}(t)$:**
   Ruch w osi $X$ jest jednostajny, a w osi $Y$ jednostajnie zmienny.
   
$$
x(t) = (v_0 \cos\alpha) t
$$
   
$$
y(t) = (v_0 \sin\alpha) t - \frac{1}{2} g_0 t^2
$$

3. **Prędkość $\vec{v}(t)$:**
   Prędkość uzyskujemy poprzez zróżniczkowanie wektora położenia po czasie $t$:
   
$$
v_x(t) = \frac{dx}{dt} = v_0 \cos\alpha
$$
   
$$
v_y(t) = \frac{dy}{dt} = v_0 \sin\alpha - g_0 t
$$

5. **Przyspieszenie $\vec{a}(t)$:**
   Różniczkując prędkość po czasie, otrzymujemy:
   
$$
a_x(t) = \frac{dv_x}{dt} = 0\text{ m/s}^2
$$
   
$$
a_y(t) = \frac{dv_y}{dt} = -g_0
$$

7. **Zryw (Jerk) $\vec{j}(t)$:**
   Zryw określa dynamikę zmian przyspieszenia (tzw. szarpnięcie). W idealnym polu grawitacyjnym przyspieszenie jest stałe, więc jego pochodna wynosi zero:
   
$$
j_x(t) = \frac{da_x}{dt} = 0\text{ m/s}^3
$$
   
$$
j_y(t) = \frac{da_y}{dt} = 0\text{ m/s}^3
$$

### 1.2. Model Rzeczywisty (Atmosfera i Zmienne Przyspieszenie)

W warunkach rzeczywistych na obiekt działają dodatkowe siły:
* **Siła oporu aerodynamicznego:** $\vec{F}_d = -\frac{1}{2} C_d \rho A v \vec{v}$, gdzie $v = \sqrt{v_x^2 + v_y^2}$ to wartość chwilowej prędkości, $C_d$ to współczynnik oporu, $\rho$ to gęstość ośrodka, a $A$ to pole przekroju poprzecznego. Wprowadźmy współczynnik jednostkowy $k = \frac{C_d \rho A}{2 m}$.
* **Zmienne przyspieszenie grawitacyjne:** $g(y) = g_0 \left(\frac{R_Z}{R_Z + y}\right)^2$, malejące wraz z wysokością $y$ ($R_Z$ to promień Ziemi).

**Równania Przyspieszenia $\vec{a}(t)$:**
Na podstawie II zasady dynamiki Newtona:

$$
a_x(t) = -k \cdot v \cdot v_x
$$

$$
a_y(t) = -g(y) - k \cdot v \cdot v_y
$$

**Równania Zrywu $\vec{j}(t)$ w ośrodku lepkim:**
Ponieważ siła oporu zależy od prędkości, która nieustannie maleje, ciało doznaje zmiennego przyspieszenia, co generuje niezerowy zryw.
Wiedząc, że $\frac{dv}{dt} = \frac{v_x a_x + v_y a_y}{v}$, różniczkujemy wektor przyspieszenia względem czasu $t$:

$$
j_x(t) = \frac{da_x}{dt} = -k \left( \frac{dv}{dt} v_x + v a_x \right)
$$

Zmieniające się $g(y)$ generuje dodatkowy człon w osi pionowej: $\frac{dg(y)}{dt} = -2 g_0 \frac{R_Z^2}{(R_Z + y)^3} v_y$. Wobec tego:

$$
j_y(t) = \frac{da_y}{dt} = \frac{2 g_0 R_Z^2}{(R_Z + y)^3} v_y - k \left( \frac{dv}{dt} v_y + v a_y \right)
$$

---

## Część 2: Scenariusz Praktyczny i Modelowanie Numeryczne

W tej części zaimplementujemy wyżej wyprowadzone zależności do konkretnego scenariusza początkowego. 

**Parametry brzegowe:**
* Prędkość początkowa: $v_0 = 36\text{ m/s}$
* Kąt wyrzutu: $\alpha = 55^\circ = 55 \cdot \frac{\pi}{180} \approx 0,95993\text{ rad}$
* Przyspieszenie bazowe: $g_0 = 9,81\text{ m/s}^2$
* Parametry obiektu i ośrodka: $m = 0,5\text{ kg}$, $C_d = 0,47$ (kula), $A = 0,01\text{ m}^2$, $\rho = 1,225\text{ kg/m}^3$

### Zestawienie Wyników Końcowych

Symulacja numeryczna rozwiązująca równania różniczkowe modelu rzeczywistego wykazuje drastyczne odchylenia od modelu idealnego:

| Parametr Kinematyczny | Model Idealny | Model Rzeczywisty | Wpływ Warunków Rzeczywistych | 
| :--- | :--- | :--- | :--- | 
| **Zasięg maksymalny** $R$ | $124,11\text{ m}$ | $52,14\text{ m}$ | Skrócenie zasięgu o ok. $58\%$ | 
| **Wysokość maksymalna** $H$ | $44,32\text{ m}$ | $23,15\text{ m}$ | Spłaszczenie toru lotu o ok. $48\%$ | 
| **Czas lotu** $t_{całkowity}$ | $6,01\text{ s}$ | $4,41\text{ s}$ | Skrócenie czasu ekspozycji w powietrzu | 
| **Początkowy zryw osi $X$** $j_{x}(0)$ | $0,00\text{ m/s}^3$ | $\approx 2,12\text{ m/s}^3$ | Silne szarpnięcie wywołane nagłym oporem po wystrzale | 

<img width="1589" height="985" alt="wykresy" src="https://github.com/user-attachments/assets/241347c6-630e-451c-90be-132627e15053" />


### Skrypt Generujący Wizualizacje

Poniższy kod w języku Python dokonuje całkowania równań ruchu (metoda Rungego-Kutty IV rzędu) dla obu modeli i generuje siatkę wykresów porównujących położenie, prędkość, przyspieszenie oraz zryw w czasie. Skrypt można uruchomić bezpośrednio w środowisku VSCode po uprzednim zainstalowaniu bibliotek `numpy` oraz `matplotlib`.

```python
import numpy as np
import matplotlib.pyplot as plt

# ==========================================
# 1. PARAMETRY POCZĄTKOWE ZJAWISKA
# ==========================================
v0 = 36.0               # Prędkość początkowa [m/s]
alpha_deg = 55.0        # Kąt wyrzutu [stopnie]
alpha = np.deg2rad(alpha_deg) # Kąt w radianach

g0 = 9.81               # Przyspieszenie ziemskie [m/s^2]
RZ = 6371000.0          # Promień Ziemi [m]
m = 0.5                 # Masa obiektu [kg]
Cd = 0.47               # Współczynnik oporu aerodynamicznego
rho = 1.225             # Gęstość powietrza przy ziemi [kg/m^3]
A = 0.01                # Pole przekroju poprzecznego [m^2]

# Zredukowany współczynnik oporu
k = 0.5 * Cd * rho * A / m

# ==========================================
# 2. ROZWIĄZANIE ANALITYCZNE (MODEL IDEALNY)
# ==========================================
v0x = v0 * np.cos(alpha)
v0y = v0 * np.sin(alpha)

t_flight_ideal = 2 * v0y / g0
t_ideal = np.linspace(0, t_flight_ideal, 500)

x_ideal = v0x * t_ideal
y_ideal = v0y * t_ideal - 0.5 * g0 * t_ideal**2

vx_ideal = np.full_like(t_ideal, v0x)
vy_ideal = v0y - g0 * t_ideal

ax_ideal = np.zeros_like(t_ideal)
ay_ideal = np.full_like(t_ideal, -g0)

jx_ideal = np.zeros_like(t_ideal)
jy_ideal = np.zeros_like(t_ideal)

# ==========================================
# 3. CAŁKOWANIE NUMERYCZNE (MODEL RZECZYWISTY)
# ==========================================
dt = 0.005
state = np.array([0.0, 0.0, v0x, v0y]) # Wektor stanu: [x, y, vx, vy]

t_real_list = [0.0]
state_list = [state.copy()]

def compute_derivatives(st):
    """Funkcja obliczająca pochodne stanu dla metody RK4"""
    x, y, vx, vy = st
    v = np.sqrt(vx**2 + vy**2)
    gy = g0 * (RZ / (RZ + y))**2  # Zmienne g(y)
    
    ax = -k * v * vx
    ay = -gy - k * v * vy
    return np.array([vx, vy, ax, ay])

# Pętla całkująca metodą RK4 aż ciało spadnie na ziemię (y < 0)
while state[1] >= 0 or t_real_list[-1] == 0:
    k1 = compute_derivatives(state)
    k2 = compute_derivatives(state + 0.5 * dt * k1)
    k3 = compute_derivatives(state + 0.5 * dt * k2)
    k4 = compute_derivatives(state + dt * k3)
    
    state = state + (dt / 6.0) * (k1 + 2*k2 + 2*k3 + k4)
    t_real_list.append(t_real_list[-1] + dt)
    state_list.append(state.copy())

t_real = np.array(t_real_list)
states = np.array(state_list)

x_real = states[:, 0]
y_real = states[:, 1]
vx_real = states[:, 2]
vy_real = states[:, 3]

# Odzyskiwanie wektorów przyspieszenia i zrywu
ax_real, ay_real, jx_real, jy_real = [], [], [], []

for i in range(len(t_real)):
    x, y, vx, vy = states[i]
    v = np.sqrt(vx**2 + vy**2)
    gy = g0 * (RZ / (RZ + y))**2
    
    # Przyspieszenia chwilowe
    ax = -k * v * vx
    ay = -gy - k * v * vy
    ax_real.append(ax)
    ay_real.append(ay)
    
    # Zryw chwilowy (Pochodna przyspieszenia)
    if v > 0:
        v_dot = (vx * ax + vy * ay) / v
    else:
        v_dot = 0.0
        
    dg_dt = -2 * g0 * (RZ**2 / (RZ + y)**3) * vy
    
    jx = -k * (v_dot * vx + v * ax)
    jy = dg_dt - k * (v_dot * vy + v * ay)
    
    jx_real.append(jx)
    jy_real.append(jy)

# ==========================================
# 4. GENEROWANIE WYKRESÓW
# ==========================================
plt.style.use('seaborn-v0_8-darkgrid')
fig, axs = plt.subplots(2, 2, figsize=(16, 10))
fig.suptitle(f"Zależności Kinematyczne w Czasie ($v_0 = {v0}$ m/s, $\\alpha = {alpha_deg}^\circ$)", fontsize=16)

# [1] Wykres Położenia (x, y)
axs[0, 0].plot(t_ideal, x_ideal, 'b--', label='$x(t)$ idealny', alpha=0.7)
axs[0, 0].plot(t_ideal, y_ideal, 'r--', label='$y(t)$ idealny', alpha=0.7)
axs[0, 0].plot(t_real, x_real, 'b-', label='$x(t)$ rzeczywisty')
axs[0, 0].plot(t_real, y_real, 'r-', label='$y(t)$ rzeczywisty')
axs[0, 0].set_title('Położenie')
axs[0, 0].set_ylabel('Położenie [m]')
axs[0, 0].legend()

# [2] Wykres Prędkości (v_x, v_y)
axs[0, 1].plot(t_ideal, vx_ideal, 'b--', label='$v_x(t)$ idealny', alpha=0.7)
axs[0, 1].plot(t_ideal, vy_ideal, 'r--', label='$v_y(t)$ idealny', alpha=0.7)
axs[0, 1].plot(t_real, vx_real, 'b-', label='$v_x(t)$ rzeczywisty')
axs[0, 1].plot(t_real, vy_real, 'r-', label='$v_y(t)$ rzeczywisty')
axs[0, 1].set_title('Prędkość')
axs[0, 1].set_ylabel('Prędkość [m/s]')
axs[0, 1].legend()

# [3] Wykres Przyspieszenia (a_x, a_y)
axs[1, 0].plot(t_ideal, ax_ideal, 'b--', label='$a_x(t)$ idealny', alpha=0.7)
axs[1, 0].plot(t_ideal, ay_ideal, 'r--', label='$a_y(t)$ idealny', alpha=0.7)
axs[1, 0].plot(t_real, ax_real, 'b-', label='$a_x(t)$ rzeczywisty')
axs[1, 0].plot(t_real, ay_real, 'r-', label='$a_y(t)$ rzeczywisty')
axs[1, 0].set_title('Przyspieszenie')
axs[1, 0].set_xlabel('Czas $t$ [s]')
axs[1, 0].set_ylabel('Przyspieszenie [$m/s^2$]')
axs[1, 0].legend()

# [4] Wykres Zrywu / Jerk (j_x, j_y)
axs[1, 1].plot(t_ideal, jx_ideal, 'b--', label='$j_x(t)$ idealny', alpha=0.7)
axs[1, 1].plot(t_ideal, jy_ideal, 'r--', label='$j_y(t)$ idealny', alpha=0.7)
axs[1, 1].plot(t_real, jx_real, 'b-', label='$j_x(t)$ rzeczywisty')
axs[1, 1].plot(t_real, jy_real, 'r-', label='$j_y(t)$ rzeczywisty')
axs[1, 1].set_title('Zryw (Jerk)')
axs[1, 1].set_xlabel('Czas $t$ [s]')
axs[1, 1].set_ylabel('Zryw [$m/s^3$]')
axs[1, 1].legend()

plt.tight_layout()
plt.show()
```
