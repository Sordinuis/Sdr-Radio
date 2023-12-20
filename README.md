# Sdr-Radio
Soft
import matplotlib.pyplot as plt
import numpy as np
from rtlsdr import RtlSdr

# Configure the RTL-SDR device
sdr = RtlSdr()
sdr.sample_rate = 2.048e6
sdr.center_freq = 95e6
sdr.gain = 'auto'

# Read samples and perform FFT
samples = sdr.read_samples(256 * 1024)
spectrum = np.fft.fft(samples)

# Plot the spectrum
plt.figure(figsize=(10, 6))
plt.plot(10 * np.log10(np.abs(spectrum)))
plt.title('RTL-SDR Spectrum')
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude (dB)')
plt.show()

# Close the RTL-SDR device
sdr.close()
