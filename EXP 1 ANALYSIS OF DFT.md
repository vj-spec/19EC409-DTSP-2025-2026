# EXP 1 :  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 
```
// ---- 1. READ AUDIO FILE ----
// Replace 'metal_detector_sample.wav' with your actual file name
[audio, fs] = wavread("C:\Users\acer\speaker_data\Dave\utt_08.wav");

// ---- 2. PRE-PROCESSING ----
// If stereo (2 rows), convert to mono by averaging
if size(audio, 1) == 2 then
    audio = mean(audio, 'r'); // average across rows
end

// Normalize audio signal to range [-1, 1]
audio = audio / max(abs(audio));
N = length(audio);

// ---- 3. PLOT TIME DOMAIN WAVEFORM ----
t = (0:N-1) / fs;

scf(0); // Open first figure window
clf();
plot(t, audio);
xtitle("Time-Domain Audio Signal", "Time (s)", "Amplitude");
xgrid();

// ---- 4. COMPUTE DFT USING FFT ----
Y = fft(audio);
// We only need the first half of the FFT (positive frequencies)
half_N = floor(N/2);
Y_mag = abs(Y(1:half_N)) / N; 
freqs = (0:half_N-1) * (fs / N);

// ---- 5. PLOT MAGNITUDE SPECTRUM ----
scf(1); // Open second figure window
clf();
plot(freqs, Y_mag);
xtitle("Magnitude Spectrum (FFT)", "Frequency (Hz)", "Magnitude");
xgrid();

// ---- 6. FIND AND PRINT DOMINANT FREQUENCIES ----
// gsort 'g' sorts globally, 'd' sorts in descending order
[sorted_mags, indices] = gsort(Y_mag, 'g', 'd');

printf("\n--- Audio Analysis ---\n");
printf("Sampling Frequency: %d Hz\n", fs);
printf("Top 5 dominant frequency components (Hz):\n");

for i = 1:5
    idx = indices(i);
    printf("%d: %.2f Hz (Magnitude: %.4f)\n", i, freqs(idx), sorted_mags(i));
end

```

# OUTPUT: 
<img width="1919" height="1140" alt="image" src="https://github.com/user-attachments/assets/e1274c43-3a2a-4bbf-a6dd-61fbe8d038b6" />

# RESULTS
Thus, the given program was executed successfully and the output is verified.
