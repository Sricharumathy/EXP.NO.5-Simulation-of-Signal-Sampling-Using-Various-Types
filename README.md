# EXP.NO.5-Simulation-of-Signal-Sampling-Using-Various-Types
Simulation of Signal Sampling Using Various Types such as</br>
    i) Ideal Sampling</br>
    ii) Natural Sampling</br>
    iii) Flat Top Sampling</br>

# AIM
Simulation of Signal Sampling Using Various Types such as</br>
    i) Ideal Sampling</br>
    ii) Natural Sampling</br>
    iii) Flat Top Sampling</br>
# SOFTWARE REQUIRED
Google Colab [Python]

# ALGORITHMS
1.Generate a sine wave signal
2.Create impulse train for ideal sampling
3.Create rectangular pulse train for natural and flat-top sampling
4.Multiply the signal with sampling pulses
5.Plot original and sampled signals

# PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt

# Common parameters
fs = 1000                          # Time resolution for plotting
t = np.linspace(0, 1, fs)          # Time vector (0 to 1 second)
f = 5                              # Frequency of sine wave (Hz)
x = np.sin(2 * np.pi * f * t)      # Input sine wave

fs_sample = 50                     # Sampling frequency
Ts = 1 / fs_sample                 # Sampling period
pulse_width = 0.01                 # Width of sampling pulses (for natural and flat-top)

# Initialize outputs
ideal_output = np.zeros_like(t)
natural_output = np.zeros_like(t)
flattop_output = np.zeros_like(t)
impulse_train = np.zeros_like(t)
rectangular_pulse_train = np.zeros_like(t)

# Sampling process
for i in np.arange(0, 1, Ts):
    idx_start = int(i * fs)
    idx_end = int((i + pulse_width) * fs)
    if idx_end >= len(t):
        idx_end = len(t) - 1

    sample_val = np.sin(2 * np.pi * f * i)

    # Ideal Sampling (impulse values)
    ideal_output[idx_start] = sample_val
    impulse_train[idx_start] = 1

    # Natural Sampling (sample × pulse)
    natural_output[idx_start:idx_end] = x[idx_start:idx_end]

    # Flat-top Sampling (hold sampled value)
    flattop_output[idx_start:idx_end] = sample_val
    rectangular_pulse_train[idx_start:idx_end] = 1

# Plotting all 3 sampling methods
plt.figure(figsize=(14, 12))

# 1. Ideal Sampling
plt.subplot(3, 1, 1)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.stem(t, ideal_output, linefmt='green', markerfmt='go', basefmt=' ')
plt.title("Ideal Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend(["Input Sine", "Ideal Sampled"])

# 2. Natural Sampling
plt.subplot(3, 1, 2)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.plot(t, natural_output, color='orange', label="Natural Sampled")
plt.title("Natural Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

# 3. Flat-Top Sampling
plt.subplot(3, 1, 3)
plt.plot(t, x, label="Input Sine Wave", color='lightgray')
plt.plot(t, flattop_output, color='red', label="Flat-Top Sampled")
plt.title("Flat-Top Sampling")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
```

# OUTPUT
![image](https://github.com/user-attachments/assets/a94ad56d-702b-4e93-815a-b4b1a7cf27fa)

 
# RESULT / CONCLUSIONS
To simulate and visualize signal sampling using three techniques: Ideal Sampling, Natural Sampling, and Flat-Top Sampling, and compare the sampled output for a given analog signal (sine wave) was verified successfully.

