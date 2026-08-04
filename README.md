# Silicon Diode I–V Characteristics

A numerical model of current flow through a silicon p-n junction, its
temperature dependence, and the effect of series resistance.

![I-V curves](diode_iv.png)

## Result

Holding forward current fixed at 10 mA and sweeping temperature from 275 K to
350 K, the forward voltage decreases linearly at:

**dV_f/dT = −2.02 mV/K**

This matches the accepted value for silicon diodes of approximately −2 mV/K.

## What this does


This models how much voltage is needed to drive a given current through a silicon p-n junction, and how that changes with temperature and series resistance. Since a diode is the simplest device you can build from doped silicon — and a transistor is essentially two of them — understanding its behavior is the foundation for understanding semiconductor devices generally.

## The physics

The Shockley diode equation relates current to applied voltage:

I = I_S · ( exp( V / (n·V_T) ) − 1 )

where V_T = kT/q is the thermal voltage (about 25.9 mV at room temperature)
and I_S is the reverse saturation current.


The number of electrons with enough thermal energy to cross the junction barrier follows a Boltzmann distribution, which falls off exponentially with barrier height. Applying forward voltage lowers the barrier, so the number of carriers that make it across grows exponentially. Since V_T ≈ 26 mV, every 60 mV multiplies the current by ten.
The saturation current depends strongly on temperature:

I_S(T) = I_S(T_ref) · (T/T_ref)³ · exp[ (E_g/nk) · (1/T_ref − 1/T) ]


Electrons need 1.12 eV to cross silicon's bandgap, while thermal energy at room temperature is only about 0.026 eV. Only the extreme tail of the energy distribution qualifies, and heating shifts that tail dramatically. The model shows I_S growing 774× between 300 K and 350 K.

Solving for voltage gives V = n·V_T·ln(I/I_S). Raising temperature increases V_T by 17% over this range, which alone would raise the required voltage — but it also increases I_S by a factor of 774, shrinking the logarithm by 29%. The second effect dominates, so forward voltage falls at −2.02 mV/K.
## Running it

    pip install numpy matplotlib
    python diode_iv.py

Produces `diode_iv.png` and prints the extracted temperature coefficient.

## What I learned

- [Be specific. Include something you got wrong at first.]
- [The 0.6 V turn-on voltage isn't a fundamental constant — it falls out of climbing nine decades of an exponential from picoamp leakage.]
- [Temperature affects the diode through two competing terms, and the intuitive one (thermal voltage rising) is the one that loses.]

---
[Aaron Suh]
