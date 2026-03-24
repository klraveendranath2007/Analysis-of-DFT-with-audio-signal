## EXP 1 B :  ANALYSIS OF DFT WITH AUDIO SIGNAL

### AIM: 
 To analyze DFT with Audio Signal  

### APPARATUS REQUIRED: 
PC installed with SCILAB/Python. 

### PROGRAM: 
#### Step 1: Install required packages
```python
!pip install -q librosa soundfile
```
#### Step 2: Upload audio file
```python
from google.colab import files
uploaded = files.upload()   # choose your .wav / .mp3 / .flac file
filename = next(iter(uploaded.keys()))
print("Uploaded:", filename)
```
#### Step 3: Load audio
```python
import librosa, librosa.display
import numpy as np
import soundfile as sf

y, sr = librosa.load(filename, sr=None, mono=True)  
duration = len(y) / sr
print(f"Sample rate = {sr} Hz, duration = {duration:.2f} s, samples = {len(y)}")
```
#### Step 4: Play audio
```python
import matplotlib.pyplot as plt

n_fft = 2**14   
Y = np.fft.rfft(y, n=n_fft)
freqs = np.fft.rfftfreq(n_fft, 1/sr)
magnitude = np.abs(Y)

plt.figure(figsize=(12,4))
plt.plot(freqs, magnitude)
plt.xlim(0, sr/2)
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.title("FFT Magnitude Spectrum (linear scale)")
plt.grid(True)
plt.show()

plt.figure(figsize=(12,4))
plt.semilogy(freqs, magnitude+1e-12)
plt.xlim(0, sr/2)
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude (log scale)")
plt.title("FFT Magnitude Spectrum (log scale)")
plt.grid(True)
plt.show()
```
#### Step 6: Top 10 dominant frequencies
```python
N = 10
idx = np.argsort(magnitude)[-N:][::-1]
print("\nTop 10 Dominant Frequencies:")
for i, k in enumerate(idx):
    print(f"{i+1:2d}. {freqs[k]:8.2f} Hz  (Magnitude = {magnitude[k]:.2e})")
Step 7: Spectrogram (STFT)
n_fft = 2048
hop_length = n_fft // 4
D = librosa.stft(y, n_fft=n_fft, hop_length=hop_length, window='hann')
S_db = librosa.amplitude_to_db(np.abs(D), ref=np.max)

plt.figure(figsize=(12,5))
librosa.display.specshow(S_db, sr=sr, hop_length=hop_length,
                         x_axis='time', y_axis='hz')
plt.colorbar(format="%+2.0f dB")
plt.title("Spectrogram (dB)")
plt.ylim(0, sr/2)
plt.show()
```
#### AUDIO :
[mixkit-ending-show-audience-clapping-478.wav](https://github.com/user-attachments/files/26217885/mixkit-ending-show-audience-clapping-478.wav)

### OUTPUT: 
<img width="586" height="291" alt="image" src="https://github.com/user-attachments/assets/e131ffc4-3375-483f-b63c-4c1a1d3d7af8" />
<img width="586" height="285" alt="image" src="https://github.com/user-attachments/assets/12f26d8f-a000-4335-91b9-c2a8739e16bc" />
<img width="691" height="609" alt="image" src="https://github.com/user-attachments/assets/048f2f21-e3c2-4887-83e2-aea010db3d02" />

### RESULT
Thus, The Analysis of DFT with Audio Signal is Verified.
