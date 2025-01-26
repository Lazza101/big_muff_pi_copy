26/01/2025
- Figured out how to simulate subcircuits, ended up creating a new project with just the subsheet I needed to sim.
- Started a SPICE model library `SPICE_MODELS.lib`, put a few BJTs in there to test the sustain stage
- Simulated and tested sustain stage using two resistors to simulate the potentiometer and tuning the values of the two to adjust the effect
- Transient simulation with varying time scale (1m to 100m) and input sine frequency (1k, 10k, 20k)
    - Got the basic gist of the effect, by adding in the decoupling cap and series resistor to the V_OUT net, shows that the centre voltage (DC bias I guess?) of the input signal goes up to between 3 and 7V depending on the potentiometer settings, then the bias decays back down to within the 0-1V envelope of the input sine. The shape of the decay is changed by switching transistor models. Tried BC547B and BC547C, saw a little change. Also tried a BD model but apparently not worth it cause they're obsolete.
- Happy with the subcircuit now that it's simulated, now to move on to the next subcircuit in the real model.