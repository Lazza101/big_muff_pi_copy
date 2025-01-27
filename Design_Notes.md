26/01/2025
- Figured out how to simulate subcircuits, ended up creating a new project with just the subsheet I needed to sim.
- Started a SPICE model library `SPICE_MODELS.lib`, put a few BJTs in there to test the sustain stage
- Simulated and tested sustain stage using two resistors to simulate the potentiometer and tuning the values of the two to adjust the effect
- Transient simulation with varying time scale (1m to 100m) and input sine frequency (1k, 10k, 20k)
    - Got the basic gist of the effect, by adding in the decoupling cap and series resistor to the V_OUT net, shows that the centre voltage (DC bias I guess?) of the input signal goes up to between 3 and 7V depending on the potentiometer settings, then the bias decays back down to within the 0-1V envelope of the input sine. The shape of the decay is changed by switching transistor models. Tried BC547B and BC547C, saw a little change. Also tried a BD model but apparently not worth it cause they're obsolete.
- Happy with the subcircuit now that it's simulated, now to move on to the next subcircuit in the real model.

27/01/2025
- Regarding the sustain effect simulation, it appears that the frequency of the input signal has an effect on the amplitude of the output signal.
- Decoupling cap and series (current limiting?) resistor permanently added to the sustain sheet. Seems that the intended sustain effect is only present on the other side of these components so makes sense to include them at least from a simulation standpoint.
- Results below over a range of input frequencies and sustain potentiometer values (frequency doesn't effect the result at 0 sustain so only one value is shown at this setting):

![max_sustain_10kHz_sine](./notes_resources/max_sustain_10kHz_sine)

*Maximum Sustain with 10kHz input wave*

![half_sustain_10kHz_sine](./notes_resources/half_sustain_10kHz_sine)

*Half Sustain with 10kHz input wave*

![no_sustain_10kHz_sine](./notes_resources/no_sustain_10kHz_sine)

*No Sustain with 10kHz input wave*

![max_sustain_20kHz_sine](./notes_resources/max_sustain_20kHz_sine)

*Maximum Sustain with 20kHz input wave*

![half_sustain_20kHz_sine](./notes_resources/half_sustain_20kHz_sine)

*Half Sustain with 20kHz input wave*

![max_sustain_2kHz_sine](./notes_resources/max_sustain_2kHz_sine)

*Maximum Sustain with 2kHz input wave*

![half_sustain_2kHz_sine](./notes_resources/half_sustain_2kHz_sine)

*Half Sustain with 2kHz input wave*

- Added the next stage of the effects chain, selected 1N914s for the diodes as suggested in the original schematic.
    - Looks like an envelope distortion kind of effect, shifts, inverts, transposes the input signal to maintain 
    an ampitude between 0-1V DC. 
    - Simulation results are wildly different when testing the stage in isolation than in a chain with the sustain.
        - In isolation it applies envelope distortion to the input signal as described above.
        - In series, the sustain output is massively attenuated and does not peak its amplitude up as it did in 
        the sustain's isolated simulation. This then gets transposed up by the envelope stage and does not get
        enveloped in the same way the input signal did in the isolated sims.

- TODO:
    - Verify which sim behaviour is correct - isolated or chained?
    - Add sim results to log
    - Add and simulate the next stage

