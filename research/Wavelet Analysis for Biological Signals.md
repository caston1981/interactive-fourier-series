

# **Technical Specification and Validation Report: Wavelet Analysis for Circadian System Modeling**

## **I. Foundational Framework: Wavelet Selection for Biological Non-Stationarity**

The analysis of biological time series, particularly those related to circadian rhythms, requires methodologies that effectively handle inherent signal non-stationarity—where frequency, amplitude, and phase characteristics fluctuate over time. Standard spectral techniques, such as the Discrete Fourier Transform (DFT), operate under a "soft assumption" of stationarity. While DFT perfectly represents the time series, non-stationarities are encoded solely within the phase spectrum, rendering them virtually impossible to interpret visually.1 Consequently, global averaging techniques fail to capture the dynamic, time-localized changes essential for understanding biological regulation.  
The Continuous Wavelet Transform (CWT) addresses this fundamental limitation by providing a localized, instantaneous measure of spectral content across both the time and frequency domains. This capability is crucial for chronobiology, enabling the detection of subtle fluctuations in the 24-hour period or the isolation of faster, ultradian patterns embedded within the daily rhythm.2

### **1.1 Wavelet Families and Functional Roles in the MVP**

The functional biological signal analysis tool requires two distinct types of wavelet transforms, each optimized for a specific task based on the biological features being analyzed 3:

#### **1.1.1 Continuous Wavelet Transform (CWT) for Oscillatory Rhythms**

For detecting, tracking, and quantifying circadian and ultradian oscillations, the CWT is mandatory. The foundation of CWT relies on complex mother wavelets, as they provide both magnitude (power) and phase information, critical for estimating the acrophase (time of peak activity) and performing cross-signal coupling analysis.4  
The standard selection for chronobiological and neuroelectrical signals is the **Complex Morlet Wavelet (CMOR)**. This wavelet is defined by a Gaussian-tapered sine wave and is highly effective for capturing periodic, potentially damping or phase-shifting, oscillations such as the ![][image1]24-hour circadian rhythm.5 The use of complex wavelets is non-negotiable for phase-dependent analyses like Wavelet Coherence.

#### **1.1.2 Discrete Wavelet Transform (DWT) for Noise Reduction and Feature Preservation**

The DWT is used primarily for efficient, multi-resolution decomposition, which facilitates non-linear denoising and targeted feature extraction. Unlike the CWT, DWT utilizes orthogonal or biorthogonal wavelets. The choice of the DWT mother wavelet depends on the signal characteristics:

* **Smooth Signals and Filtering:** Wavelets with higher regularity, such as the **Symlets** family or higher-order **Daubechies** wavelets, are preferred when the goal is smooth low-pass filtering, trend removal, and robust denoising.3  
* **Sharp/Transient Events:** For signals containing abrupt changes or sharp discontinuities, such as behavioral onset or physiological spikes, wavelets with **shorter support**, like the **Haar** wavelet or low-vanishing moment Daubechies wavelets, are more appropriate as they minimize smoothing and better localize the transient event in time.3

### **1.2 Optimal Parameter Tuning for Circadian Analysis**

The scientific rigor of CWT analysis relies heavily on the correct parameterization of the Complex Morlet Wavelet, as this determines the fundamental trade-off between time resolution (localization of an event) and frequency resolution (accuracy of the period estimate).1

#### **1.2.1 Morlet Parameterization and FWHM Clarity**

The Complex Morlet Wavelet is frequently parameterized by the "number of cycles" (![][image1] or ![][image1]), which controls the width of the Gaussian envelope. Relying solely on this parameter can be mathematically opaque and introduce uncertainty or suboptimal choices.1 A superior approach for ensuring clarity and reproducibility is parameterizing the wavelets directly in terms of  
**Full-Width at Half-Maximum (FWHM)** in both the temporal and spectral domains. This formulation explicitly links the mathematical parameter to the desired temporal and spectral smoothing, leading to more robust results.1  
For standard circadian analysis, a conventional starting point for the Morlet center frequency parameter is often ![][image1]. This selection provides an empirically robust balance, allowing the wavelet sufficient oscillations within its localization window to achieve adequate frequency precision while maintaining reasonable temporal resolution necessary for chronobiological data analysis.6

#### **1.2.2 Scale Selection and Cone of Influence**

The CWT uses the scale parameter (![][image1]) to map the wavelet frequency content to the signal's pseudo-period (![][image1]). The relationship is approximately given by ![][image1], where the center frequency ![][image1].5  
For analyzing biological oscillations, the scale vector must span the relevant periodicities, typically ranging from ultradian (periods of a few hours) up to multi-day (infradian, 72 hours). The scales are typically chosen logarithmically, based on the sampling frequency, to capture the 24-hour cycle and its sub-harmonics accurately.7  
A critical technical consideration is the **Cone of Influence (COI)**. Due to the finite length of the time series and the necessity of zero-padding for computational efficiency, edge effects occur where the spectral power estimates are unreliable. The COI defines this boundary in the time-frequency plane. Any spectral power or coherence results within the COI must be explicitly masked during visualization and statistical interpretation to prevent artifacts from being mistaken for valid biological signals.8

## **II. Phase I: Advanced Biological Denoising and Feature Extraction (DWT)**

The first phase of signal processing involves using the DWT to implement a superior, non-linear filtering mechanism that isolates noise while preserving the intricate dynamics and sharp features of biological time series. This method offers a decisive advantage over standard linear bandpass filters, which tend to smooth out vital transient events.2 Implementing DWT denoising requires an adaptive, data-driven optimization of the mother wavelet, the decomposition level, and the thresholding rule.

### **2.1 The DWT Decomposition Strategy and Optimal Level Selection**

The DWT decomposes the signal into Approximation (![][image1]) and Detail (![][image1]) coefficients across multiple levels ![][image1]. Noise primarily resides in the highest-frequency detail coefficients (![][image1]).9 The critical challenge is determining the optimal decomposition level  
![][image1]. An arbitrary choice of ![][image1] based purely on signal length risks insufficient noise removal (if ![][image1] is too low) or, conversely, signal distortion and over-denoising (if ![][image1] is too high, leaking signal energy into the coefficients targeted for removal).10

#### **2.1.1 Adaptive Level Determination**

The expert-level approach mandates an adaptive level selection pipeline based on rigorous statistical validation and performance optimization:

1. **Noise Fidelity Validation (Jarque–Bera Test):** Before thresholding, the decomposition must be validated. The Jarque–Bera test is employed on the highest frequency detail coefficient (![][image1]) to ensure that the extracted component statistically conforms to the characteristics of Gaussian white noise.10 This step confirms that the decomposition process has successfully isolated true, structureless noise, thereby guaranteeing that the fundamental assumption required for effective Universal or Stein thresholding is met. If the test fails, it suggests signal components are still leaking into the noise level, necessitating optimization or reconsideration of the mother wavelet choice.  
2. **Performance Optimization (Composite Metric):** To objectively determine the best level ![][image1], an iterative evaluation of potential levels is performed using a single, composite metric. This metric combines standard error indicators, such as Root Mean Square Error (RMSE), with dimensional metrics like signal smoothness.10 A composite weighting strategy—combining the entropy weight method and the coefficient of variation method—is utilized to integrate these otherwise disparate metrics into a single, comprehensive evaluation index. Minimizing this composite index accurately determines the optimal decomposition level, leading to smoother peak regions and more stable reconstructed waveforms than traditional methods.10

### **2.2 Optimal Mother Wavelet Selection using Sparsity**

Effective DWT denoising hinges on selecting a mother wavelet that maximizes the separation between signal and noise coefficients in the wavelet domain.11 A trial-and-error approach is insufficient for a rigorous technical tool.  
The required methodology involves selecting the optimal basis using the **Mean of Sparsity Change (![][image1])** parameter.11 This technique mandates calculating the sparsity of the detail components across a predefined collection of candidate wavelets (e.g., Daubechies, Symlets). The wavelet yielding the highest  
![][image1] value is selected because it maximizes the compression of the signal into the fewest coefficients, thereby maximizing the separation of coefficients related to the signal structure from coefficients related to the noise.11 This quantitative approach eliminates subjective biases often present in heuristic wavelet selection.

### **2.3 Robust Thresholding Techniques**

Once the optimal basis and level are chosen, robust thresholding must be applied to the detail coefficients.

* **Threshold Type:** **Soft thresholding** is generally recommended for biological signal processing. It shrinks the wavelet coefficients toward zero, resulting in a significantly smoother and more stable reconstructed waveform, mitigating the introduction of artificial discontinuities often caused by hard thresholding.12  
* **Validated Threshold Rules:** The toolkit must support threshold determination methods validated for minimizing error in the presence of biological noise:  
  * **Universal Threshold (VisuShrink):** This baseline method, defined by MAD×2log(m)​ (where MAD is the Median Absolute Deviation and ![][image1] is signal length), is widely used and robust when the noise variance is unknown.12  
  * **Stein's Unbiased Risk Estimator (SureShrink):** This adaptive method is optimized for minimizing the overall Mean Squared Error (MSE), providing superior performance when the underlying noise characteristics are accurately estimated, which is facilitated by the Jarque–Bera test validation.12

### **2.4 DWT Detrending as a Preprocessing Step**

A substantial advantage of DWT over traditional filters is its inherent ability to perform time-localized detrending. Biological time series frequently contain slow baseline shifts or trends (![][image1] currents, metabolic drift).12 By isolating the approximation coefficients (  
![][image1])—which represent the lowest frequency components—the DWT effectively captures this trend. To prepare the signal for accurate CWT analysis, the final reconstructed signal is generated using only the thresholded detail coefficients (![][image1]), implicitly removing the low-frequency drift component ![][image1]. This wavelet-based detrending is superior to simple high-pass filtering or polynomial fitting because it is localized in time and defined by the optimal decomposition level ![][image1].

## **III. Phase II: Bivariate Analysis and Synchronization (Wavelet Coherence)**

Wavelet coherence (WC) is the essential advanced feature of the MVP, providing the ability to quantify the time-and-frequency localized phase coupling and synchronization between two related biological signals (e.g., input stimuli and response, or coupled gene expression rhythms).

### **3.1 Cross-Wavelet Transform and Wavelet Coherence Calculation**

The process begins with the Cross-Wavelet Transform (XWT), which identifies regions in the time-frequency domain where two signals, ![][image1] and ![][image1], share significant common power. The XWT ![][image1] is defined as the product of the complex CWT of ![][image1] and the complex conjugate of the CWT of ![][image1]:  
![][image1]While XWT shows common power, Wavelet Coherence (![][image1]) quantifies the strength of the linear correlation or covariance between the two signals, normalized to a value between 0 (no correlation) and 1 (perfect correlation). This is achieved by smoothing the XWT and normalizing it by the product of the smoothed individual power spectra:  
![][image1]  
where S represents a smoothing operator in both time and scale.8

### **3.2 Statistical Significance Testing and Null Models**

The non-stationary nature of biological data makes standard analytical statistical tests for coherence invalid.13 Robust scientific interpretation demands statistically validated significance regions using Monte Carlo randomization techniques.8

1. **Null Hypothesis Selection:** For biological and environmental time series, which exhibit strong autocorrelation, the default null hypothesis must be the **Red Noise Null Hypothesis (AR(1) process)**.13 Assuming a simpler white noise model when analyzing autocorrelated data dramatically inflates the perceived statistical significance (increasing Type I error rate).  
2. **Procedure:** The Monte Carlo method involves generating a large ensemble of surrogate time series pairs (e.g., ![][image1]) that possess the same intrinsic autocorrelation structure as the input data but are randomized in their phase relationships (destroying any true coupling).  
3. **Thresholding:** The Wavelet Coherence ![][image1] is calculated for every surrogate pair. This distribution establishes the ![][image1] significance level. Only coherence values exceeding this threshold in the original data are considered statistically significant, and only these regions should be considered for biological interpretation.8

### **3.3 Interpretation of Wavelet Coherence Phase**

The phase angle ![][image1] derived from the complex WC values provides crucial information regarding the relative timing of the two synchronized signals (lead/lag) within the statistically significant regions.8 This phase relationship is vital for inferring potential regulatory flow or structural coupling within a biological system.8  
The phase is typically visualized using arrows overlaid on the coherence spectrum. The direction of the arrows indicates the timing relationship:  
Table III. Wavelet Coherence Phase Interpretation Guide (Biological Systems)

| Phase Arrow Direction | Phase Angle (![][image1]) | Interpretation | Biological Implication |
| :---- | :---- | :---- | :---- |
| Right (![][image1]) | ![][image1] | In-phase synchronization. | Direct co-regulation or simultaneous activation/inhibition. |
| Up (![][image1]) | ![][image1] (![][image1]) | X leads Y by one-quarter cycle (![][image1]). | X signal is upstream, driving Y later in the rhythmic process. |
| Left (![][image1]) | ![][image1] (![][image1]) | Anti-phase synchronization. | Inverse relationship (e.g., activator X peaking as inhibitor Y troughs). |
| Down (![][image1]) | ![][image1] (![][image1]) | Y leads X by one-quarter cycle (![][image1]). | Y signal is upstream, driving X later in the rhythmic process. |

This analysis allows for the detection of structural coupling, such as between functional regions of small GTPases in protein dynamics 8, or the regulatory flow between central and peripheral circadian clocks. It is essential to remember that phase information is only biologically meaningful within the bounds of the statistically significant coherence regions.14 Furthermore, the analysis should focus on interpreting results across multiple relevant time scales (ultradian to circadian), as synchronization can occur transiently at different periodicities, representing rapid feedback loops or secondary biological oscillations.2

## **IV. Implementation Framework: Python Libraries and Performance**

The development of the functional MVP tool requires a carefully selected Python ecosystem to balance high-speed computation with specialized statistical robustness.

### **4.1 Hybrid Python Stack Rationale**

The analysis pipeline requires a hybrid structure utilizing two specialized libraries:

* **PyWavelets (pywt):** This serves as the high-performance core engine. PyWavelets offers highly optimized (C/Cython backend) implementations for both DWT (pywt.wavedec, pywt.waverec) and 1D Continuous Wavelet Transforms (pywt.cwt). This performance capability is essential for handling large biological time series datasets efficiently.15 PyWavelets supports over 100 built-in wavelet filters, facilitating the required adaptive basis selection for denoising.15  
* **PyCWT (pycwt):** While PyWavelets handles the core CWT calculation, specialized libraries such as PyCWT are essential for the statistically demanding aspects of bivariate analysis. PyCWT provides pre-optimized routines for calculating Cross-Wavelet Transform, Wavelet Coherence, and critically, the statistically rigorous Monte Carlo significance testing against red noise models, which PyWavelets does not natively specialize in.13

**Note on SciPy:** Development teams must be aware that the general-purpose scipy.signal.cwt function has been officially deprecated since SciPy version 1.12.0. All CWT operations should be standardized on the more robust and future-proof PyWavelets library.18

### **4.2 Computational Performance and Optimization**

Wavelet analysis, especially the CWT across a wide range of scales, can be computationally intensive. Optimization must be considered upfront for large biological datasets.  
The computational complexity of the Discrete Wavelet Transform (DWT) using the Mallat algorithm scales linearly, ![][image1], where ![][image1] is the number of data points. However, the Continuous Wavelet Transform (CWT) implemented using the Fast Fourier Transform (FFT) algorithm scales as ![][image1] per scale. If ![][image1] scales are analyzed, the total complexity is ![][image1].18  
Optimization strategies include:

1. **FFT Implementation:** Ensure all CWT calculations utilize the fast convolution theorem (via FFT), which both PyWavelets and PyCWT employ.  
2. **Scale Vector Logarithmic Spacing:** To reduce the number of scales (![][image1]) without sacrificing coverage of the target rhythm, the scale vector should be logarithmically spaced and centered around the periods of biological interest (e.g., ![][image1] hours to ![][image1] hours) rather than using linear or excessively fine spacing across the entire frequency range.  
3. **Data Type Management:** Use single-precision floating-point arithmetic wherever possible, reserving double precision only for critical statistical calculations to optimize memory usage and processing speed.

### **4.3 Modular Implementation Requirements**

The MVP architecture must enforce a sequential pipeline to ensure data integrity and maximize the effectiveness of specialized methods:

1. **Denoising and Detrending Module:** The signal must first pass through the DWT adaptive optimization pipeline (Section 2.1) to remove high-frequency noise and low-frequency trend (![][image1] removal). This step ensures the subsequent CWT operates on a clean, detrended signal, improving rhythm detection accuracy.  
2. **CWT Module:** This module handles the Complex Morlet Wavelet application, focusing on FWHM parameterization (as discussed in Section 1.2.1), scale vector generation, and the initial calculation of the time-averaged wavelet power spectrum for rhythm detection.  
3. **Coherence Module:** This module integrates PyCWT functionalities for XWT, WC, and the mandatory Monte Carlo simulation against the Red Noise Null Hypothesis, providing both the raw coherence matrix and the statistically masked results.

## **V. Quantitative Validation and Benchmarking**

The MVP must quantitatively demonstrate that wavelet methods provide measurable superiority over traditional linear filtering and global spectral analysis. This requires defining specific performance metrics and utilizing validated benchmark datasets.

### **5.1 Validation Datasets and Ground Truth Definition**

Rigorous validation requires both synthesized data (for absolute ground truth) and real-world experimental data (for consensus validation).

1. **Synthetic Data (Absolute Ground Truth):** Simulated signals are the primary benchmark, as they provide an absolute ground truth for period, phase, and the characteristics of non-stationarity (e.g., known damping rates or sudden period shifts). This allows for precise calculation of errors and metrics like SNR improvement and the recovery of hidden features.19  
2. **Open Access Experimental Data (Consensus Ground Truth):** Validation must extend to real biological complexity using established public repositories. The resources provided by the Society for Research on Biological Rhythms (SRBR) are essential, including access to BioDare2 (a repository sharing over 10,000 public experiments with analysis tools) and CircaDB (Circadian Gene Expression Data Base).20 These databases contain time-series data for locomotor activity, RNA expression (e.g.,  
   *Per1* or *Bmal1*), and other physiological variables. The "ground truth" for these experimental datasets is defined as the consensus rhythm parameters established by multiple validated chronobiological analysis tools (such as Lomb-Scargle, MESA, and Cosinor analysis).21

### **5.2 Metrics for Quantitative Improvement**

Validation must focus on metrics that specifically highlight the advantages of time-frequency localization and non-linear filtering:

1. **Noise Mitigation Metrics:**  
   * **SNR Improvement:** Quantitative measurement of the Signal-to-Noise Ratio increase achieved by the DWT denoising process.  
   * **Sparsity Improvement (![][image1]):** Measurement of the change in the Mean of Sparsity Change before and after denoising. A greater improvement quantitatively validates the success of the optimal wavelet selection in segregating noise from structured signal components, confirming feature preservation.11  
2. **Rhythm Detection Metrics:**  
   * **Period Accuracy:** Error (in hours or minutes) between the estimated period and the ground truth. Crucially, CWT must be validated for its ability to track **instantaneous period changes** over time, a task traditional methods cannot perform.2  
   * **Feature Resolution (Sensitivity/Specificity):** Quantitative assessment of the tool's ability to detect and accurately resolve simultaneous periodicities, particularly embedded **ultradian components** (e.g., high-frequency feeding or activity bouts), which Fourier periodograms often fail to separate from the dominant 24-hour cycle.2  
3. **Temporal Event Localization:** For transient events, metrics must demonstrate superior localization sensitivity (e.g., timing of activity onset/offset) compared to simple differentiation or linear smoothing techniques.

### **5.3 Wavelet Superiority Proof: Head-to-Head Comparison**

The quantitative superiority of wavelet analysis justifies its increased complexity by excelling in areas where traditional global methods fundamentally fail.  
Traditional methods, including the DFT and Cosinor analysis, assume the signal is constant or perfectly sinusoidal.22 This causes them to average out and obscure time-varying dynamics, such as damping or phase shifts, which are ubiquitous in biological systems.2  
Table IV demonstrates the measured quantitative advantages:  
Table IV. Performance Comparison: Wavelets vs. Traditional Methods for Chronobiology

| Metric/Feature | Traditional Methods (Fourier/Cosinor) | Wavelet Transform (CWT/DWT) | Quantitative Advantage of Wavelets |
| :---- | :---- | :---- | :---- |
| **Non-Stationary Data Handling** | Poor: Assumes stationarity (Global spectral average). | Excellent: Provides time-localized spectral estimates. | Precisely tracks instantaneous period shifts and dynamic amplitude damping.2 |
| **Ultradian Rhythm Detection** | Poor: High-frequency components obscured by dominant rhythm. | Excellent: Resolves multi-frequency structure (e.g., 4-hour and 24-hour cycles simultaneously). | Higher sensitivity and specificity for identifying complex, simultaneous frequency patterns.2 |
| **Noise Filtering Technique** | Linear Bandpass Filtering (often distorts transients). | Non-linear Thresholding (Adaptive DWT). | Preserves sharp transients (onsets/offsets) while maximizing SNR improvement.3 |
| **Statistical Rigor for Coupling** | Cross-correlation/Coherence lacks time-frequency specificity. | Wavelet Coherence with Monte Carlo/Red Noise significance testing. | Provides statistically validated correlation across specific time periods and scales, reducing Type I errors.8 |

The superiority of the CWT is most apparent in detecting time-dependent changes—such as when a circadian rhythm begins to shift or dampen over several days in constant conditions.2 Furthermore, the DWT provides a targeted, non-linear filter that avoids the smoothing inherent in linear bandpass methods, quantitatively improving the Signal-to-Noise Ratio while ensuring the preservation of essential biological features like activity onsets.

## **VI. Conclusions and Technical Recommendations**

The development of a functional biological signal analysis tool leveraging wavelet transforms requires a specialized, adaptive, and statistically rigorous approach that fundamentally moves beyond the limitations of traditional fixed-filter and global spectral analysis.  
The analysis confirms that the Complex Morlet Wavelet (CMOR) is the validated method for Circadian Rhythm detection, requiring a standardized parameterization (ideally FWHM-based) and mandatory masking of the Cone of Influence. For noise removal, the Discrete Wavelet Transform (DWT) offers quantifiable improvements over linear filtering, but only if an adaptive optimization pipeline is implemented. This pipeline must integrate the ![][image1] parameter for optimal mother wavelet selection, and utilize the Jarque–Bera test combined with a composite error metric for robust, distortion-free level selection.  
For bivariate analysis, the MVP must rely on the Wavelet Coherence technique, making the use of complex wavelets essential for phase tracking. The scientific validity of all coupling results rests entirely on implementing Monte Carlo statistical significance testing based on the **Red Noise Null Hypothesis (AR(1) process)**, ensuring the results are not spuriously inflated by inherent biological autocorrelation.  
The MVP should be constructed as a hybrid Python framework, utilizing the performance of **PyWavelets** for core transforms and DWT denoising, and leveraging the statistical specialization of **PyCWT** for the rigorous implementation of XWT, WC, and Monte Carlo validation against the required red noise model. Validation must be performed against both synthetic signals (absolute ground truth) and established chronobiology datasets (consensus ground truth) using metrics that specifically measure the preservation of transients and the detection of time-varying frequency shifts.

#### **Works cited**

1. A better way to define and describe Morlet wavelets for time-frequency analysis \- bioRxiv, accessed October 1, 2025, [https://www.biorxiv.org/content/10.1101/397182v1.full](https://www.biorxiv.org/content/10.1101/397182v1.full)  
2. Wavelet analysis of circadian and ultradian behavioral rhythms \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC3717080/](https://pmc.ncbi.nlm.nih.gov/articles/PMC3717080/)  
3. Choice of Wavelet Bases | Signal Processing Class Notes \- Fiveable, accessed October 1, 2025, [https://fiveable.me/fourier-analysis-wavelets-and-signal-processing/unit-11/choice-wavelet-bases/study-guide/pQOZSQ0e4q8FNr3r](https://fiveable.me/fourier-analysis-wavelets-and-signal-processing/unit-11/choice-wavelet-bases/study-guide/pQOZSQ0e4q8FNr3r)  
4. A Practical Guide to Wavelet Analysis \- NOAA, accessed October 1, 2025, [https://psl.noaa.gov/people/gilbert.p.compo/Torrence\_compo1998.pdf](https://psl.noaa.gov/people/gilbert.p.compo/Torrence_compo1998.pdf)  
5. Optimal time frequency analysis for biological data \- pyBOAT \- bioRxiv, accessed October 1, 2025, [https://www.biorxiv.org/content/10.1101/2020.04.29.067744v2.full-text](https://www.biorxiv.org/content/10.1101/2020.04.29.067744v2.full-text)  
6. Cycle selection in Morlet wavelet analysis \- Google Groups, accessed October 1, 2025, [https://groups.google.com/g/analyzingneuraltimeseriesdata/c/ljwEPhihRj4](https://groups.google.com/g/analyzingneuraltimeseriesdata/c/ljwEPhihRj4)  
7. Circadian cycles: A time-series approach \- SciELO México, accessed October 1, 2025, [https://www.scielo.org.mx/scielo.php?script=sci\_arttext\&pid=S0035-001X2023000500013](https://www.scielo.org.mx/scielo.php?script=sci_arttext&pid=S0035-001X2023000500013)  
8. Wavelet coherence phase analysis decodes the universal switching mechanism of Ras GTPase superfamily \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC10336170/](https://pmc.ncbi.nlm.nih.gov/articles/PMC10336170/)  
9. Optimal level and order of the Coiflets wavelet in the VAR time series denoise analysis \- Frontiers, accessed October 1, 2025, [https://www.frontiersin.org/journals/applied-mathematics-and-statistics/articles/10.3389/fams.2025.1526540/full](https://www.frontiersin.org/journals/applied-mathematics-and-statistics/articles/10.3389/fams.2025.1526540/full)  
10. Determination Method of Optimal Decomposition Level of Discrete Wavelet Based on Joint Jarque–Bera Test and Combination Weighting Method \- MDPI, accessed October 1, 2025, [https://www.mdpi.com/1099-4300/27/2/108](https://www.mdpi.com/1099-4300/27/2/108)  
11. Optimal Wavelet Selection for Signal Denoising \- PMC \- National Institutes of Health (NIH) |, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC11486496/](https://pmc.ncbi.nlm.nih.gov/articles/PMC11486496/)  
12. gdetor/wavelet\_denoising: A simple Python implementation of basic Wavelet denoising algorithms \- GitHub, accessed October 1, 2025, [https://github.com/gdetor/wavelet\_denoising](https://github.com/gdetor/wavelet_denoising)  
13. Wavelet analysis in ecology and epidemiology: impact of statistical tests \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC3869155/](https://pmc.ncbi.nlm.nih.gov/articles/PMC3869155/)  
14. Coherence and Phase Relationship Analysis of the Two Main Frequency Components of EHG, as Observed by Complex Wavelet Transform \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/226186469\_Coherence\_and\_Phase\_Relationship\_Analysis\_of\_the\_Two\_Main\_Frequency\_Components\_of\_EHG\_as\_Observed\_by\_Complex\_Wavelet\_Transform](https://www.researchgate.net/publication/226186469_Coherence_and_Phase_Relationship_Analysis_of_the_Two_Main_Frequency_Components_of_EHG_as_Observed_by_Complex_Wavelet_Transform)  
15. PyWavelets \- Wavelet Transforms in Python — PyWavelets Documentation, accessed October 1, 2025, [https://pywavelets.readthedocs.io/](https://pywavelets.readthedocs.io/)  
16. PyWavelets \- Wavelet Transforms in Python \- GitHub, accessed October 1, 2025, [https://github.com/PyWavelets/pywt](https://github.com/PyWavelets/pywt)  
17. PyCWT: spectral analysis using wavelets in Python, accessed October 1, 2025, [https://pycwt.readthedocs.io/](https://pycwt.readthedocs.io/)  
18. scipy.signal.cwt — SciPy v1.12.0 Manual, accessed October 1, 2025, [https://docs.scipy.org/doc/scipy-1.12.0/reference/generated/scipy.signal.cwt.html](https://docs.scipy.org/doc/scipy-1.12.0/reference/generated/scipy.signal.cwt.html)  
19. Access to ground truth at unconstrained size makes simulated data as indispensable as experimental data for bioinformatics methods development and benchmarking, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9620827/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9620827/)  
20. Research tools | SRBR: Society for Research on Biological Rhythms, accessed October 1, 2025, [https://srbr.org/education-outreach/research-tools/](https://srbr.org/education-outreach/research-tools/)  
21. (PDF) Wavelet-Based Analysis of Circadian Behavioral Rhythms \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/272098563\_Wavelet-Based\_Analysis\_of\_Circadian\_Behavioral\_Rhythms](https://www.researchgate.net/publication/272098563_Wavelet-Based_Analysis_of_Circadian_Behavioral_Rhythms)  
22. Procedures for numerical analysis of circadian rhythms \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC3663600/](https://pmc.ncbi.nlm.nih.gov/articles/PMC3663600/)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAYAAACtWK6eAAAAsUlEQVR4Xu3BAQEAAACCIP+vbkhAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAB8GXHmAAEdo+NeAAAAAElFTkSuQmCC>