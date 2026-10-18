# Rzut ukośny: porównanie z i bez oporu powietrza

![Wykres porównania rzutu ukośnego z i bez oporu powietrza](wykres.png)

## Wprowadzenie
Wykres przedstawia tor lotu ciała rzuconego ukośnie w dwóch modelach: $v_0$ przy założeniu braku oporu powietrza oraz przy uwzględnieniu siły oporu. W idealnym modelu ruch jest opisany prostą parabolą, natomiast w rzeczywistych warunkach tor lotu ulega odkształceniu przez $g$ i opór aerodynamiczny. Warto zauważyć, że $\theta$ ma kluczowy wpływ na zasięg i wysokość maksymalną.

## Interpretacja wykresu
Wyniki pokazują, że przy tym samym kącie i prędkości początkowej ciało rzucone bez oporu osiąga większy zasięg oraz wyższą maksymalną wysokość niż ciało poruszające się w ośrodku z oporem. W praktyce oznacza to, że **opór powietrza zmniejsza energię ruchu**, a przez to skraca czas lotu i obniża trajektorię. Dodatkowo, *niewielki wpływ oporu jest najbardziej widoczny na końcowym odcinku toru*.

- większa wysokość maksymalna bez oporu,
- dłuższy zasięg przy idealnym rzucie,
- zniekształcenie toru pod wpływem oporu,
- asymetria przebiegu wynikająca z hamowania ruchu.

1. Załóżmy stałą prędkość początkową $v_0$.
2. Ustalmy kąt wyrzutu $\theta$.
3. Porównaj zasięg i wysokość dla dwóch modeli.
4. Przeanalizuj wpływ siły oporu na tor lotu.

- [ ] sprawdzono model bez oporu,
- [ ] sprawdzono model z oporem,
- [ ] porównano zasięg i wysokość,
- [ ] zanotowano wnioski.

| Model | Zasięg (m) | Wysokość maksymalna (m) |
|---|---:|---:|
| Bez oporu powietrza | 255 | 65 |
| Z oporem powietrza | 120 | 43 |

Link do strony Google Colab: http://colab.research.google.com

```python
import numpy as np

v0 = 50.0
theta = np.deg2rad(45)
g = 9.81

t = np.linspace(0, 2 * v0 * np.sin(theta) / g, 200)
x = v0 * np.cos(theta) * t
y = v0 * np.sin(theta) * t - 0.5 * g * t**2
```

W modelu idealnym można opisać tor lotu równaniem $y(x) = x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}$, a zasięg wynosi $R = \frac{v_0^2 \sin(2\theta)}{g}$. Dla ruchu z oporem stosuje się często zależność $F_d = \frac{1}{2} C_d \rho A v^2$, gdzie $C_d$ to współczynnik oporu.

$$
y(x) = x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}
$$

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

$$
F_d = \frac{1}{2} C_d \rho A v^2
$$

## Podsumowanie
Wniosek jest prosty: ~~w idealnym modelu tor lotu zawsze jest parabolą~~, ale w realnym świecie opór powietrza zmienia trajektorię i zmniejsza osiągi. Dlatego analiza wykresu pozwala lepiej zrozumieć, dlaczego *ruch w atmosferze różni się od modelu idealnego*.
