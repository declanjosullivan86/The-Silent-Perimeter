When investigating acoustic harassment or tech-facilitated surveillance, the goal is **objective documentation**. Standard microphones often have "filters" that cut out very low or very high frequencies; therefore, forensic analysis requires tools that can visualize the full raw spectrum.

The following table lists Python-based libraries, scripts, and open-source tools specifically suited for detecting anomalies, recording high-fidelity audio, and performing spectral analysis.

### Forensic Audio & Analysis Tools

| Project / Tool Name | Language / Platform | Primary Forensic Use Case | Link |
| :--- | :--- | :--- | :--- |
| **Librosa** | Python | Analyzing audio signals for rhythmic patterns, pitch tracking, and spectral features. | [GitHub](https://github.com/librosa/librosa) |
| **Sonic Visualiser** | C++ (Open Source) | **Highly Recommended.** Visualizing subtle "hidden" frequencies (spectrograms) that the human ear may miss. | [Website](https://www.sonicvisualiser.org/) |
| **Audio-Forensics** | Python | A collection of scripts for detecting audio tampering and identifying recording environments. | [GitHub](https://github.com/pndurette/audio-forensics) |
| **PyAudio Analysis** | Python | Feature extraction and classification. Can be used to "train" a script to alert you when a specific frequency starts. | [GitHub](https://github.com/tyiannak/pyAudioAnalysis) |
| **Scipy Signal** | Python | Essential for "Band-pass Filtering." Use this to isolate infrasound (low) or ultrasound (high) frequencies. | [Documentation](https://docs.scipy.org/doc/scipy/reference/signal.html) |
| **Spleeter** | Python | AI-based stem separation. Useful for isolating voices from heavy background noise or "masking" sounds. | [GitHub](https://github.com/deezer/spleeter) |
| **Spectrum Analyzer** | Python/Qt | Real-time spectral visualization to monitor for live acoustic pulses or persistent signals. | [GitHub](https://github.com/chidiwilliams/buzz) |
| **BatScanner / Ultrasound** | Python | Scripts designed for high-frequency detection (often used in bioacoustics but applicable to tech surveillance). | [GitHub](https://github.com/petervojtek/batscanner) |
| **Audacity** | C++ (Open Source) | The standard for long-form recording and manual noise reduction/analysis. | [GitHub](https://github.com/audacity/audacity) |

---

### Technical Recommendations for Forensic Recording

If you are documenting acoustic harassment for legal or safety purposes, keep these technical constraints in mind:

1.  **Hardware Limits:** Most smartphone microphones are designed to ignore frequencies below 20Hz (Infrasound) and above 18kHz (Ultrasound). If you suspect "silent" harassment, you may need an **omni-directional measurement microphone** (like a UMIK-1) that has a flat response across a wider range.
2.  **Long-Form Recording:** For intermittent harassment, use a script based on `PyAudio` to record only when sound crosses a certain decibel threshold to save disk space while capturing "events."
3.  **The Spectrogram is Key:** When presenting evidence to colleagues or authorities, a **Spectrogram** (a heat map of frequency over time) is more effective than an audio file. It visually proves a signal exists even if the listener's ears cannot perceive it.
4.  **Calibration:** Always record a "control" (the room when it is completely silent and the suspected device/harassment is off) to compare against the "event" recordings.

### Example Python Snippet for Simple Frequency Detection
You can use this basic structure with `numpy` and `scipy` to check for specific high-frequency "pings" in a recording:

```python
import numpy as np
from scipy.io import wavfile
from scipy.fft import fft

def detect_frequency(file_path):
    fs, data = wavfile.read(file_path)
    # Perform Fast Fourier Transform
    n = len(data)
    p = fft(data) 
    mag = np.abs(p)
    freqs = np.fft.fftfreq(n, 1/fs)
    
    # Identify peak frequency
    idx = np.argmax(mag)
    peak_freq = freqs[idx]
    print(f"Peak Frequency Detected: {abs(peak_freq)} Hz")

# Usage: detect_frequency('suspicious_noise.wav')
```

**Legal Disclaimer:** Ensure you are compliant with local "one-party consent" or "two-party consent" recording laws. While documenting harassment for your own safety is often protected, check local regulations regarding the use of recorded evidence in court.
