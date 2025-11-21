# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 
```
# Install dependencies if not already available
!pip install scipy matplotlib

import numpy as np
import matplotlib.pyplot as plt
from scipy.io import wavfile
from google.colab import files

# Step 1: Upload audio file
print("Please upload a .wav file")
uploaded = files.upload()

filename = list(uploaded.keys())[0]  # Get uploaded filename
fs, data = wavfile.read(filename)    # Read audio
print("Sampling Frequency:", fs)

# If stereo, convert to mono
if data.ndim > 1:
    data = data[:, 0]

# Step 2: Compute FFT
N = len(data)
freq = np.fft.fftfreq(N, 1/fs)
spectrum = np.fft.fft(data)

# Step 3: Filter - remove frequencies above 3000 Hz
cutoff = 3000
spectrum_filtered = spectrum.copy()
spectrum_filtered[np.abs(freq) > cutoff] = 0

# Step 4: Reconstruct signal (Inverse FFT)
filtered_data = np.fft.ifft(spectrum_filtered).real.astype(np.int16)

# Step 5: Save filtered audio
output_filename = "filtered_audio.wav"
wavfile.write(output_filename, fs, filtered_data)

# Download filtered file
files.download(output_filename)

# Step 6: Plot spectrum before and after filtering
plt.figure(figsize=(12,6))

plt.subplot(2,1,1)
plt.title("Original Signal Spectrum")
plt.plot(freq[:N//2], np.abs(spectrum[:N//2]))
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")

plt.subplot(2,1,2)
plt.title("Filtered Signal Spectrum")
plt.plot(freq[:N//2], np.abs(spectrum_filtered[:N//2]))
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")

plt.tight_layout()
plt.show()
```

# OUTPUT: 
<img width="1188" height="590" alt="image" src="https://github.com/user-attachments/assets/8b79230d-e44f-45a6-a100-799132953441" />



# RESULTS
Hence ANALYSIS OF DFT WITH AUDIO SIGNAL is done successfully.
