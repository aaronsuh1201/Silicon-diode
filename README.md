# Silicon Diode I–V Characteristics

A numerical model of current flow through a silicon p-n junction, its
temperature dependence, and the effect of series resistance.

![I-V curves](diode_iv.png)

## Result

**Figure 1 — I–V characteristic at 300 K.**
The modeled current rises exponentially with forward voltage, with no
threshold in the equation itself. Current becomes visible on a linear
scale near [0.6] V, but this is a plotting artifact rather than a
physical turn-on point.

**Figure 2 — Semi-log I–V characteristic.**
Plotted on a log current axis, the forward region is a straight line,
confirming the exponential form. The slope corresponds to roughly
60 mV per decade of current at room temperature — i.e. current changes
by a factor of 10 for every 60 mV of applied voltage. Over the range
plotted, current spans approximately [N] decades.

**Figure 3 — Forward voltage vs. temperature at fixed current.**
Holding forward current fixed at 10 mA and sweeping temperature from
275 K to 350 K, forward voltage falls approximately linearly:

dV_f/dT = −2.02 mV/K

This agrees with the accepted value for silicon diodes of roughly
−2 mV/K.

The negative sign reflects two competing temperature effects. The
thermal voltage V_T = kT/q rises with temperature, which alone would
require *higher* forward voltage to hold current constant. But the
saturation current I_S rises far more steeply, since I_S ∝ n_i² and
n_i² ∝ T³·exp(−E_g/kT). The I_S term dominates, so forward voltage
must fall to keep current fixed. Because E_g/q is the largest term in
the analytical expression, this temperature coefficient is effectively
an indirect measurement of the silicon band gap.

## What this does

This models how much voltage is needed to drive a given current through a silicon p-n junction, and how that changes with temperature and series resistance.

## The physics

The Shockley diode equation relates current to applied voltage:

I = I_S · ( exp( V / (n·V_T) ) − 1 )

where V_T = kT/q is the thermal voltage (about 25.9 mV at room temperature)
and I_S is the reverse saturation current.

[Why is the relationship exponential?]

Electron energies follow a Boltzmann distribution, so the fraction with enough energy to cross the junction barrier falls off exponentially with barrier height. Forward voltage lowers that barrier, so the number of carriers crossing rises exponentially with applied voltage.

[What does the −1 term do?]

Without the −1, the equation would predict current flowing with zero voltage applied. A free energy machine. The −1 makes them cancel exactly.

[Why does a diode conduct almost nothing until about 0.6 V?]

0.6V is the volatge required for the electrons to overcome the depletion region and flow through the diode. Rearranging the diode equation shows that multiplying the current by a factor of ten costs about 60 mV of additional forward voltage. Moving from picoamps of background leakage to milliamps of operating current spans nine factors of ten. Multiplying nine factors of ten by 60 mV yields 540 mV, or about 0.54 V. Because of this, a diode with a larger initial leakage current requires fewer factors of ten to reach operating current, which causes it to turn on at a lower voltage. 
The saturation current depends strongly on temperature:

I_S(T) = I_S(T_ref) · (T/T_ref)³ · exp[ (E_g/nk) · (1/T_ref − 1/T) ]

[Why does heating a semiconductor free more carriers? What role is the
bandgap playing?]

Electrons in silicon are bound and can't conduct until they absorb enough energy to cross the bandgap — 1.12 eV. Thermal energy at room temperature is only ~0.026 eV, so only electrons in the high tail of the energy distribution make it. therefore when temperature increases energy of electrons increases freeing exponentially more carriers.


[Why does the diode turn on at a LOWER voltage when it's hotter, even
though you might expect more resistance?]


Temperature affects the required voltage in two competing ways. As the diode gets hotter, thermal voltage rises by 17%, which on its own would require a higher voltage. However, the background leakage current grows so rapidly that it shrinks the logarithmic part of the equation by 29%. Since the second effect dominates, the net result is that forward voltage falls at −2.02 mV/K.
## Running it

    pip install numpy matplotlib
    python diode_iv.py

Produces `diode_iv.png` and prints the extracted temperature coefficient.

## What I learned

- [unlike metal where higher temperature rather increases the resistance, in diode, higher temperature lowers the voltage required to have electrons flow thorugh. lowering resistance. ]
- [thermal energy increases the probability of a charge having enough energy to cross a barrier of height ]

---
Aaron Suh
