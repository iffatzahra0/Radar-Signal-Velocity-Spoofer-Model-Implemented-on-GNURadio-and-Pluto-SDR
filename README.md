# Radar-Signal-Velocity-Spoofer-Model-Implemented-on-GNURadio-and-Pluto-SDR
---
This project demonstrates a radar signal velocity spoofing experiment using two Pluto SDRs and a Vector Signal Generator (VSG).  

- **One Pluto SDR** is used for reception and determining velocity.  
- **The second Pluto SDR** is used for transmitting a spoofed 3.5 GHz signal.  

The received signal is successfully processed in the flowgraph, and the outputs are visualized in the *RADAR_SIGNAL_VELOCITY_SPOOFER.png*.  

---

## 🔹 GNU Radio Flowgraph Overview

Below is the function of each block in the system:

1. **Pluto Source**  
   - Receives the incoming signal from the Vector Signal Generator.  

2. **DC Blocker**  
   - Removes any constant (DC) offset component from the received signal, ensuring only the dynamic frequency content is analyzed.  

3. **Log Power FFT**  
   - Computes the Fast Fourier Transform (FFT) of the signal and outputs the power spectrum in dB scale.  
   - Used here to identify the dominant peak frequency.  

4. **Argmax**  
   - Finds the index of the maximum power value in the FFT output (i.e., the strongest frequency component).  

5. **Short to Float**  
   - Converts the `short` data type from Argmax into `float` for subsequent numerical processing.  

6. **Multiply Constant**  
   - Scales the FFT index by `(samp_rate / fft_size)` to convert it into an actual frequency value (in Hz).  

7. **Constant Source 1**  
   - Provides the modulation frequency offset that is subtracted from the measured frequency in order to calculate the true frequency shift.  

8. **Constant Source 2**  
   - Implements the Doppler velocity formula:  
 v = shift * speed of light / 2 * carrier frequency

---

## 📊 Outputs
- The system outputs the calculated velocity values based on the frequency shift caused by spoofing.  
- Visualization of the processing chain can be found in `RADAR_SIGNAL_VELOCITY_SPOOFER.png`.  

---



---
