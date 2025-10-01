# BioXen Four-Lens Interactive App - Quick Start Guide

## 🚀 Getting Started

Open `bioxen-lenses.html` in your web browser to explore the interactive four-lens analysis system for biological signals.

---

## 📍 Navigation Guide

### Main Sections (Left Sidebar)

1. **Overview** - Introduction to the four-lens system
2. **Fourier Lens** - Steady-state periodic analysis (Lomb-Scargle)
3. **Wavelet Lens** ⭐ NEW - Time-frequency localization for non-stationary signals
4. **Laplace Lens** - System stability and feedback control
5. **Z-Transform Lens** - Discrete-time filtering
6. **Interactive Demo** - Compare all four lenses on realistic scenarios
7. **Validation Tools** - Check if your data meets scientific requirements
8. **Implementation** - Technical architecture and dependencies
9. **Roadmap** - Development phases and future features

---

## 🎮 Interactive Features

### 1. Decision Tree (Overview Section)
**Purpose:** Help you choose the right lens for your data

**How to use:**
1. Click "Yes - Non-stationary" if your signal's frequency changes over time
2. Click "No - Stationary" if frequency is constant
3. See recommendation with scientific reasoning

**Example scenarios:**
- Cell transitioning through cell cycle phases → Non-stationary (use Wavelet)
- Stable circadian rhythm → Stationary (use Fourier)

---

### 2. Fourier Analysis Demo (Fourier Section)
**Purpose:** Compare uniform vs irregular sampling methods

**Interactive controls:**
- **Sampling selector:** Toggle between "Uniform (FFT)" and "Irregular (Lomb-Scargle)"
- **Add Noise button:** Add/remove measurement noise to test robustness
- **Run Spectral Analysis:** Calculate dominant period and confidence

**Try this:**
1. Select "Uniform Sampling" → Run Analysis → See FFT result
2. Select "Irregular Sampling" → Run Analysis → See Lomb-Scargle handles missing data
3. Add Noise → Notice Lomb-Scargle maintains confidence score

**What you'll learn:** Why Lomb-Scargle is essential for real biological data

---

### 3. Wavelet Analysis Demo (Wavelet Section)
**Purpose:** Visualize how wavelets detect transient events

**Interactive controls:**
- **Signal Type buttons:**
  - **Stress Response:** Sudden frequency shift (stress event at t=5s)
  - **Damping Oscillation:** Decaying amplitude (dying cell)
  - **Frequency Shift:** Gradual frequency increase (chirp)
- **Show Fourier Comparison:** Reveals Fourier's limitation (loses timing info)

**Try this:**
1. Click "Stress Response" → See sudden frequency jump in scalogram
2. Click "Show Fourier Comparison" → Notice Fourier averages everything (can't detect when shift occurred)
3. Try "Damping Oscillation" → See amplitude decay over time

**What you'll learn:** Why Fourier fails on non-stationary signals

---

### 4. Four-Lens Comparison (Interactive Demo Section)
**Purpose:** See how each lens reveals different insights on the same data

**Interactive controls:**
- **Scenario buttons:**
  - **Circadian Rhythm:** Stable 24h periodic cycle
  - **Stress Event:** Transient response to environmental shock
  - **Feedback Control:** Homeostasis maintaining steady state
  - **Noisy Data:** Real-world measurement challenges

**Try this:**
1. Click "Stress Event" scenario
2. Read the four lens results:
   - Fourier: Detects multiple frequencies but misses timing
   - **Wavelet: CRITICAL - Shows exact moment of frequency shift** ⭐
   - Laplace: Pole movement indicates system instability
   - Z-Transform: Kalman filter tracks state transitions
3. Read summary to understand when each lens is essential

**What you'll learn:** Multi-lens analysis is necessary for comprehensive understanding

---

### 5. Validation Checker (Validation Section)
**Purpose:** Ensure your data meets scientific requirements before analysis

**Interactive controls:**
- **Sampling Rate input:** How many samples per second
- **Expected Max Frequency input:** Highest frequency in your signal
- **Run Validation Checks button:** See pass/fail results

**Try this:**
1. Set Sampling Rate = 1.0 Hz, Max Frequency = 0.1 Hz
   - Result: ✅ PASS (Nyquist satisfied: 1.0 > 2×0.1)
2. Set Sampling Rate = 0.1 Hz, Max Frequency = 1.0 Hz
   - Result: ❌ FAIL (Nyquist violated: Need 2.0 Hz minimum!)

**What you'll learn:** Nyquist criterion prevents aliasing errors

---

## 🎯 Recommended Learning Path

### Beginner (15 minutes)
1. Read **Overview** section
2. Use **Decision Tree** to understand lens selection
3. Try **Fourier Demo** - Toggle uniform vs irregular sampling
4. Try **Wavelet Demo** - Click "Stress Response" signal

### Intermediate (30 minutes)
1. Complete Beginner path
2. Explore **Four-Lens Comparison** - Try all 4 scenarios
3. Use **Validation Checker** - Test different sampling rates
4. Read **Implementation** section for technical details

### Advanced (60 minutes)
1. Complete Intermediate path
2. Read full **Fourier**, **Wavelet**, **Laplace**, **Z-Transform** sections
3. Review **Roadmap** for advanced features (HOSA, State-space)
4. Click footer links to research papers for deep dive

---

## 💡 Key Concepts to Understand

### 1. Non-Stationarity
- **Definition:** Signal's frequency content changes over time
- **Example:** Cell transitioning from G1 to S phase has different metabolic frequencies
- **Solution:** Use Wavelet lens instead of Fourier

### 2. Irregular Sampling
- **Definition:** Measurements at uneven time intervals (missing data points)
- **Example:** Sensor malfunction, instrument downtime
- **Solution:** Use Lomb-Scargle instead of standard FFT

### 3. Nyquist Criterion
- **Definition:** Sampling rate must be ≥ 2× maximum frequency
- **Example:** To detect 1 Hz oscillations, sample at ≥ 2 Hz
- **Solution:** Use Validation Checker before analysis

### 4. Time-Frequency Localization
- **Definition:** Knowing both WHEN and WHAT frequency occurs
- **Example:** Stress response at exactly t=5.2 seconds
- **Solution:** Wavelet scalogram shows this; Fourier cannot

---

## 🔍 Common Questions

### Q: Which lens should I use?
**A:** Use the Decision Tree! General rules:
- Stable periodic signal → Fourier
- Changing frequency → Wavelet
- System control → Laplace
- Sampled data filtering → Z-Transform
- **Best practice:** Use all four for comprehensive analysis

### Q: Why can't I just use FFT for everything?
**A:** FFT assumptions:
- ✅ Works: Uniform sampling, stationary signal
- ❌ Fails: Irregular sampling, non-stationary signal
- Try the Fourier Demo to see the difference!

### Q: What's a scalogram?
**A:** Time-frequency plot from wavelet analysis
- **X-axis:** Time
- **Y-axis:** Frequency (scale)
- **Color/Height:** Signal strength at that time-frequency
- Shows HOW frequency content evolves over time

### Q: Why does biological data need special treatment?
**A:** Biological signals are:
- Non-stationary (cells change states)
- Irregularly sampled (equipment issues)
- Noisy (molecular stochasticity)
- **Standard methods (FFT) assume none of these!**

---

## 🎨 Visual Legend

### Color Coding
- **Purple** 🟣 - Fourier lens
- **Cyan** 🔵 - Wavelet lens (NEW)
- **Orange** 🟠 - Laplace lens
- **Green** 🟢 - Z-Transform lens
- **Blue** 🔷 - General information
- **Amber** 🟡 - Warnings/updates
- **Red** 🔴 - Errors/failures
- **Green** ✅ - Success/pass

### Icons
- 🌊 - Fourier (wave-like)
- 📈 - Wavelet (time-frequency)
- ⚙️ - Laplace (mechanical control)
- 📊 - Z-Transform (discrete data)
- ⭐ - New feature
- 🔬 - Scientific/research
- 🎯 - Key concept
- 💡 - Learning tip

---

## 🛠️ Troubleshooting

### Charts not displaying?
- **Solution:** Ensure internet connection (loads Chart.js from CDN)
- Check browser console for errors

### Interactive buttons not responding?
- **Solution:** Refresh page, ensure JavaScript enabled
- Try different browser (Chrome, Firefox recommended)

### Mobile layout issues?
- **Solution:** Use sidebar toggle (hamburger icon)
- Rotate to landscape for better chart viewing

---

## 📚 Further Reading

### In-App Resources (Footer Links)
1. **Biology Frequency Domain Review** - Peer-reviewed applications
2. **Mathematical Foundations** - Rigorous transform theory
3. **Research Addendum** - Latest enhancements and upgrades

### Key Papers (mentioned in app)
- Van Dongen: Lomb-Scargle Periodogram for circadian analysis
- Wu et al.: MetaCycle multi-algorithm approach
- Del Vecchio & Murray: Control theory for biological systems

---

## 🎓 Learning Outcomes

After exploring this app, you should be able to:

✅ Explain the four-lens analysis framework  
✅ Choose the appropriate lens for your biological data  
✅ Understand why Fourier fails on non-stationary signals  
✅ Validate data using Nyquist criterion  
✅ Interpret wavelet scalograms  
✅ Compare uniform vs irregular sampling methods  
✅ Recognize when multi-lens analysis is essential  

---

## 🚀 Next Steps

1. **Experiment:** Try different scenarios and parameter combinations
2. **Apply:** Use decision tree for your actual biological data
3. **Validate:** Check your sampling rate before analysis
4. **Integrate:** Reference implementation section for BioXen code
5. **Learn More:** Click research paper links in footer

---

**Pro Tip:** The app is designed for hands-on learning. Don't just read—**click everything** and observe how the visualizations change! 🎮

---

**Version:** 2.0  
**Last Updated:** October 2025  
**For Issues:** See REFACTORING_SUMMARY.md for technical details
