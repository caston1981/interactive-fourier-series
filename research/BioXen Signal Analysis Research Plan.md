

# **Production-Grade Implementation of the BioXen Four-Lens Signal Analysis System for Biological Temporal Dynamics**

## **I. Strategic Overview and Scientific Mandate**

The BioXen Four-Lens Signal Analysis system is designed to fulfill the requirements of modern systems biology, moving beyond reductionist approaches to holistically understand and model the dynamic properties of cells, tissues, and organisms.1 This shift in perspective, traceable back to Aristotle’s philosophy that "the totality is not, as it were, a mere heap, but the whole is something besides the parts," requires sophisticated computational frameworks.1 Analyzing biological temporal dynamics—ranging from high-frequency hormone pulses to daily circadian rhythms and complex cell cycles 2—demands mathematical rigor to characterize oscillation, track transients, and infer causal mechanisms.

### **A. The Systems Biology Imperative**

Systems biology necessitates advanced tools because it focuses on the interaction of components rather than the components themselves.1 Historically, this field has been built on foundational mathematical models of dynamic processes, such as Balthasar van der Pol’s relaxation oscillations used for theoretical models of neuronal systems, and the seminal work by Hodgkin and Huxley describing the action potential.1 Modern systems biology, enabled by high-throughput data generation and advanced computational processing power, requires analytic lenses capable of dissecting intertwined feedback loops that govern phenomena like rhythmicity and robustness in biological clocks.1  
The complexity of biological data—often noisy, non-sinusoidal, and sampled irregularly—renders traditional, simplistic analysis inadequate. The BioXen mandate addresses this by implementing a layered, multi-domain approach. Crucially, the system must translate rhythm detection (Lenses 1 and 2\) and transient localization (Lens 3\) into verifiable causal models (Lens 4). The explicit inclusion of the Laplace and Z-Transforms (Lens 4\) is the technical manifestation of the systems biology paradigm within BioXen, enabling the derivation of transfer functions that model feedback and control.3

### **B. Establishing Peer-Reviewed Standards for Biological Rhythmometry**

For the BioXen system to achieve production-grade status suitable for generating peer-reviewed results, it must adhere to stringent formal guidelines and consensus regarding best practices for large-scale data generation and analysis.5 The primary objective is to increase the rigor and reproducibility of research in chronobiology and computational biology.5  
This necessitates robust statistical validation and comprehensive quality control. Published results must properly account for the inherent uncertainty associated with large-scale experiments.5 A core expectation in the field is efficiency, accuracy, and the elimination of human error in interpretation, as demonstrated by the benchmarking and open-source deployment of tools like Rhythmidia, developed for calculating circadian periods from experimental data sets.6 Reliance on a single algorithm output is risky, given that different methods possess unique strengths and weaknesses depending on the noise level, curve shape, and sampling rate of the input data.9 Therefore, BioXen’s architecture must implicitly incorporate a multi-algorithmic consensus logic to validate results, ensuring the derived period and statistical significance are robust across different mathematical perspectives.

### **C. BioXen Four-Lens System Architectural Mandate**

The BioXen system is structured around four distinct mathematical transformations, each targeting a specific class of information embedded within the temporal biological data:  
BioXen Four-Lens System Architectural Mandate

| Analysis Lens | Mathematical Domain | Biological Question Addressed | Systems Biology Contribution |
| :---- | :---- | :---- | :---- |
| Lens 1/2: Fourier & LSP | Frequency Domain | Global Periodicity (![][image1]) and Strength (Power) | Characterization of stable, inherent rhythms (e.g., circadian period). |
| Lens 3: Wavelet Transform | Time-Frequency Domain | Transient Dynamics, Non-stationarity | Localization of specific phases or transient shifts (e.g., cell cycle progression, perturbation response). |
| Lens 4: Laplace & Z-Transform | System Dynamics Domain | Causal Inference, Transfer Function | Mechanistic modeling of feedback loops and stability analysis (e.g., genetic circuit gain/delay). |

## **II. Lens 1 & 2: Frequency Domain Analysis (Fourier and Lomb-Scargle)**

Frequency domain analysis provides the fundamental metrics of rhythmicity, defining the period (![][image1]) and the spectral power. While the Fast Fourier Transform (FFT) is computationally efficient, it is unsuitable as the sole production-grade tool due to its intrinsic limitations concerning biological data.

### **A. Standard Fourier Analysis (FFT) Limitations**

Standard FFT and related methods, such as Fisher's G Test, require time series data that is complete and evenly sampled.10 This assumption often fails in biological research due where measurements are frequently unequally spaced or incomplete due to experimental constraints or subject variability.11 Failure to meet these criteria can lead to potential 'mode failure' in detection, resulting in unreliable or artifactual peak detection.10 The necessity for a robust solution that can reliably analyze time series regardless of sampling regularity is paramount for achieving peer-reviewed rigor.5

### **B. The Superiority of Generalized Lomb-Scargle (GLSP)**

The Lomb-Scargle Periodogram (LSP) is established as the most versatile method available for the detection and evaluation of biological rhythms, particularly because it performs a least-squares frequency analysis tailored for unequally spaced data.11 It statistically resolves issues related to spectral leakage and aliasing that confound standard periodograms when sampling is irregular.11 LSP has proven effective in differentiating between periodic and non-periodic profiles even when the data is high in noise or has a low sampling rate.10  
For a production-grade system, BioXen must implement the **Generalized Lomb-Scargle Periodogram (GLSP)**, also known as the floating-mean periodogram.12 Traditional LSP assumes a signal mean of zero, an assumption rarely valid in biological systems where baseline activity or constitutive expression levels are significant. The GLSP accounts for the floating mean, which is mathematically superior as it provides more accurate frequencies, is less susceptible to aliasing, and yields a superior determination of spectral intensity compared to the classical LSP variant.12 Mandating the GLSP ensures that the fundamental rhythmic component is identified against an accurately determined biological baseline.

### **C. Production Implementation and Triangulation**

The Python implementation relies on sophisticated packages capable of handling the statistical requirements of GLSP, such as the astropy.timeseries.LombScargle module, which includes functionality for fitting the floating mean.12 Output metrics must include the detected period (  
![][image1]), the peak power, and a rigorous statistical significance metric, typically the False Alarm Probability (FAP) or the P-value.  
To satisfy peer-reviewed standards for robustness, the BioXen architecture must employ a multi-algorithmic validation scheme for period detection. Since the optimal algorithm depends inherently on the unknown features of the data (such as oscillation shape) 10, reliance on the GLSP alone is insufficient. The final period determination module must concurrently run a triad of proven approaches: (1) Generalized LSP (handling uneven sampling), (2) JTK\_CYCLE (effective for differentiating between periodic and non-periodic data, especially with high noise and non-sinusoidal curves) 10, and (3) a generalized Fourier cosine fit (serving as a statistical baseline comparator). This multi-algorithmic comparison forms the critical initial layer of the Consensus Validation Module detailed in Section V.

## **III. Lens 3: Multi-Resolution Analysis (The Wavelet Transform)**

While spectral analysis identifies a dominant global period, the Continuous Wavelet Transform (CWT) provides essential localization in the time-frequency domain. This is necessary for analyzing non-stationary biological signals where periodicity or amplitude changes over time, or where transient events occur.

### **A. Continuous Wavelet Transform (CWT) Theory**

CWT achieves simultaneous resolution in both time and frequency (or scale), making it ideal for processes governed by multiple interacting time scales or processes involving sharp transitions, such as the cell cycle.13 For example, CWT enables the detailed tracking and temporal quantification of distinct phases (G1, S, G2/M) within the cell cycle, where the length of each phase constitutes a crucial temporal feature.13 The CWT output, the scalogram, maps biological events by scale, allowing discrimination between fast hormonal pulses and slower, intrinsic rhythms.  
The ability of CWT to localize rhythm components precisely in time provides a critical bridge to the System Dynamics lens (Lens 4). By identifying the exact temporal coordinates where phase shifts or amplitude dampening occur, the Wavelet analysis informs the causality models on where system parameters (such as gain or delay) might be dynamically changing in response to stimuli or internal feedback.

### **B. Optimal Mother Wavelet Selection Strategy**

A fundamental challenge in implementing a production-grade Wavelet analysis system is the extreme dependence of performance on the choice of the mother wavelet (e.g., Morlet, Daubechies, Coiflet).14 This selection cannot be heuristic; it must be optimized to match the specific characteristics of the input signal, considering properties such as symmetry, smoothness, and the number of vanishing moments.15  
BioXen must incorporate an empirical, data-driven optimization routine to select the most suitable mother wavelet for each input dataset.  
One robust method involves selecting the wavelet that maximizes the **sparsity** of the Detail components in the wavelet domain.16 This process maximizes the separation of noise coefficients from signal coefficients, a critical step for effective denoising and signal extraction, especially when dealing with low Signal-to-Noise Ratio (SNR) data.16 The system calculates the mean of sparsity change (  
![][image1]), and selects the wavelet (or a collection of the top five wavelets) with the highest ![][image1] value.16 For low SNR data, the system must be particularly stringent, as only a few wavelets may efficiently denoise the signal; conversely, high SNR data may tolerate a wider range of effective wavelets.16  
Alternative criteria used in biomedical signal processing include the Evaluation Criterion (EC), which sums the absolute value of CWT coefficients across all scales.14 For high-quality signals, wavelets with higher vanishing moments, such as specific orders of Daubechies (Db) or Coiflet families, are often preferred as they yield sparser representations for smoother signals and images.14 For complex biological time series, Db44 has been identified as an optimal choice in certain biomedical contexts based on EC maximization.14  
BioXen Mother Wavelet Selection Criteria

| Criterion | Wavelet Property Assessed | Mathematical Basis | Optimal Selection (BioXen Action) |
| :---- | :---- | :---- | :---- |
| Sparsity Change (![][image1]) | Separation of Signal/Noise Coefficients | Maximizes signal concentration in the fewest coefficients (sparsity of Detail components).16 | Select wavelet with highest ![][image1], particularly critical for low SNR data.16 |
| Evaluation Criterion (EC) | Continuous Wavelet Coefficient Amplitude | Summation of absolute CWT coefficient values across all scales.14 | Select wavelet that maximizes EC for feature extraction stability. |
| Vanishing Moments | Signal Reconstruction Fidelity | Determines capacity to represent polynomials of a certain degree; increases sparsity for smooth signals.15 | Choose higher-order wavelets (Db, Coiflet) for smoother, less distorted signals.14 |

### **C. Python Implementation**

The Python implementation must leverage pywt (PyWavelets) for CWT generation. Crucially, the system must include an initial, automated module that iterates over a pre-selected library of wavelets (potentially 66 families, as suggested in prior studies, assessed based on vanishing moment and regularity properties 14) to compute the  
![][image1] for the input data, ensuring the subsequent time-frequency analysis is performed with the mathematically optimal basis function.

## **IV. Lens 4: System Dynamics and Network Inference (Laplace and Z-Transforms)**

The final and most crucial component of the BioXen system for meeting the systems biology mandate is the shift from descriptive analysis (rhythm detection) to predictive, mechanistic modeling through system identification. This is achieved using the Laplace and Z-Transforms to derive transfer functions that define causal relationships within biological networks.4

### **A. The Foundation in Control Theory**

Biological networks, such as circadian clocks or cell cycle regulation, function as complex feedback control circuits. The Laplace and Z-Transforms provide the tools necessary for **system identification**—the process of empirically describing linear dynamic models by fitting unknown coefficients to observed input-output relationships.4

### **B. Continuous-Time Modeling with Laplace Transform**

The Laplace Transform is primarily used for theoretical analysis of continuous, time-invariant systems, expressed in the ![][image1]\-domain (where ![][image1] is the Laplace variable).4 This is critical for deriving theoretical transfer functions  
![][image1] for idealized biological circuits, such as genetic feedback loops.3  
Analysis in the ![][image1]\-domain allows for the quantification of operational parameters within a negative feedback setup. Key parameters include **gain (![][image1])**, which may represent the local slope of the Hill function or the strength of transcription factor regulation, and **delay (![][image1])**, which arises from intrinsic uncertainties or time lags in biomolecular interactions.3 Furthermore, stability analysis (e.g., using root locus or Bode plots in the  
![][image1]\-domain) provides a mechanistic assessment of the system's robustness and capacity to sustain oscillation.

### **C. Discrete-Time Modeling with Z-Transform**

Since empirical biological data is universally collected as a discrete-time series, the Z-Transform is essential for applied model fitting.4 It deals with difference equations and discrete transfer functions  
![][image1], where ![][image1] is the discrete-time variable.4  
Biological networks are frequently Multiple-Input, Multiple-Output (MIMO) systems.4 Identifying these complex interactions—which may involve multivariate interactions, co-linearity of inputs, and significant data processing 4—requires Z-Transform based methods. These methods fit linear dynamic models such as discrete transfer functions or state-space representations (defined by matrices A, B, C, D).4 Specialized Python libraries such as  
python-control or optimization frameworks like GEKKO 4 are required for solving this dynamic model identification problem.

### **D. Advanced Diagnostic Filter: Higher-Order Spectral Analysis (HOSA)**

While the Laplace and Z-Transforms are powerful for linear analysis, biological reality is often governed by nonlinear processes (e.g., genetic regulation via Hill functions).3 To maintain peer-reviewed rigor, the BioXen system must explicitly validate whether the linear Z-Transform approximation is justifiable for a given dataset.  
The system incorporates an **Advanced Diagnostic Filter** based on Higher-Order Spectral Analysis (HOSA), including Bispectrum and Bicoherence estimation.17 HOSA detects non-Gaussianity and non-linear interactions. Specifically, Bicoherence measures quadratic phase coupling between frequency components. A significant Bicoherence value indicates strong non-linear coupling, signaling that the underlying biological process cannot be adequately described by a simple linear transfer function derived from the Z-Transform.17 This diagnostic step elevates BioXen from a standard analysis tool to an expert-level mechanistic platform, confirming the validity of its system models or flagging the necessity for implementing more complex non-linear modeling techniques (e.g., Volterra series, non-linear state-space models).

## **V. Production-Grade Architecture and Validation**

The robustness and utility of the BioXen Four-Lens System depend on its integrated architecture, rigorous statistical validation, and adherence to N-version programming principles.

### **A. BioXen Integrated Workflow and Software Stack**

The production workflow begins with standardized data ingestion, followed by essential preprocessing steps including normalization, detrending, and baseline subtraction, which maximize the fidelity of subsequent mathematical transformations.  
The Python stack for the BioXen system is defined by specialized libraries optimized for efficiency and mathematical rigor:  
Python Library Implementation Matrix for BioXen Production

| Analysis Technique | Primary Python Library | Key Functions/Methods | Role in BioXen System |
| :---- | :---- | :---- | :---- |
| LSP (Generalized) | astropy.timeseries | LombScargle(..., fit\_mean=True) | Primary spectral detection for unequally spaced data.11 |
| CWT/Wavelet Optimization | pywt | cwt, Custom ![][image1] calculation | Time-frequency localization and scale analysis.16 |
| Z-Transform/System ID | python-control | tf, ss, c2d (Continuous to Discrete) | Empirical MIMO modeling of biological networks.4 |
| HOSA Diagnostics | spectrum | bispectrum\_direct, bicoherence | Non-linear coupling detection and model validation.17 |
| Statistical Correction | statsmodels, scipy.stats | multipletests (FDR control) | Consensus scoring and rigor management.5 |

### **B. N-Version Programming and Consensus Logic (MetaCycle Architecture)**

To ensure maximum statistical reliability and minimize consensus error among parallel algorithms—a principle applied in robust multi-agent systems 18—BioXen adopts the N-version programming concept prevalent in advanced computational biology packages.10 This mitigates the risk of 'mode failure' where a single algorithm yields an inaccurate result due to data features it is not optimized to handle.10  
The system must run its mandated suite of rhythm detection algorithms concurrently (e.g., GLSP, JTK\_CYCLE, and a non-parametric method). Following the logic established by systems like MetaCycle 10, BioXen integrates the period estimate, phase, and raw P-value from each independent algorithm. This data is then subjected to a unified statistical assessment.  
The output is a robust **Consensus Q-value**, calculated by aggregating the P-values and applying a stringent False Discovery Rate (FDR) correction (e.g., Benjamini-Hochberg procedure). This Consensus Q-value is the definitive metric for rhythm detection rigor, ensuring that the final accepted rhythmicity profile passes a threshold appropriate for peer-reviewed publication (e.g., ![][image1]).5  
BioXen Consensus Scorecard and Algorithm Triangulation

| Metric | LSP Result | JTK\_CYCLE Result | Cosine Fit Result | Consensus Output |
| :---- | :---- | :---- | :---- | :---- |
| Period (h) | 24.1 ![][image1] 0.2 | 24.0 ![][image1] 0.3 | 24.2 ![][image1] 0.5 | 24.09 (Weighted Mean) |
| P-value | 0.001 | 0.005 | 0.02 | N/A |
| Raw Algorithm Rank | 1 | 2 | 3 | N/A |
| **Final Consensus Q-value** | N/A | N/A | N/A | \< 0.005 (PASS) |
| Note | Best for irregular sampling 11 | Best for non-sinusoidal curve 10 | Baseline fit | Required for peer-reviewed acceptance 5 |

### **C. Signal Quality and Confidence Metrics**

For any production-grade system, comprehensive output reporting is required. BioXen must quantify both the biological characteristics of the rhythm and the confidence in the mathematical model.

1. **Periodicity Metrics:** Output includes the definitive Period (![][image1]), the Amplitude (quantifying rhythm strength), and the Phase (![][image1])—a critical measure for comparing internal synchrony across components or tissues.2  
2. **Validation Metrics:** The primary metric is the Consensus Q-value (FDR corrected), which dictates statistical acceptance.5 The Goodness-of-Fit (  
   ![][image1]) statistic is also necessary to measure how closely the derived rhythm fit (whether cosine curve or transfer function model) matches the raw experimental data. Additionally, the Sparsity Score (![][image1]) from Lens 3 is reported to document the empirical process of mother wavelet selection.16

### **D. Usability and Elimination of Interpretation Error**

While the underlying mathematics is complex, the output must be accessible. The system must incorporate a simple User-Computer Interface (GUI), similar in function to modern tools like Rhythmidia.6 This interface is crucial for handling large data sets, automating complex calculations, and facilitating the visualization of multi-algorithmic consensus results. By eliminating the necessity for manually performing dozens of measurements and calculations—a process prone to human error 7—the BioXen system directly reinforces the goal of increasing rigor and reproducibility in published research.5

## **VI. Conclusions and Deployment Recommendations**

The BioXen Four-Lens system represents a robust, production-grade architecture capable of addressing the complex temporal dynamics inherent in systems biology. By mandating the Generalized Lomb-Scargle Periodogram (GLSP) for spectral analysis 11, incorporating an empirical optimization step for Continuous Wavelet Transform (CWT) analysis 16, and employing Laplace/Z-Transforms for mechanistic system identification 4, the system successfully moves beyond simple detection.  
The most critical architectural feature is the incorporation of N-version programming and Consensus Q-value scoring.10 This multi-algorithmic validation ensures that the results satisfy the rigorous statistical standards necessary for peer review, properly accounting for the inherent uncertainty of large-scale experiments.5 The integration of Higher-Order Spectral Analysis (HOSA) further provides a necessary diagnostic layer to validate the applicability of linear dynamic models, ensuring that the system identification methods adhere to expert-level diagnostic standards.17

### **Future Directions and Scalability**

1. **High-Throughput Scalability:** BioXen is designed to scale with modern ‘-omics’ approaches.1 The system must be optimized to process high-throughput datasets (e.g., large-scale transcriptomic or proteomic profiles where thousands of genes are analyzed for rhythmicity).19 This requires efficient memory management and leveraging Python’s numerical processing capabilities for vectorization (Numpy) and parallel processing, particularly for the computationally intensive CWT and the N-version consensus loop.  
2. **Open Science and Reproducibility:** To maximize scientific impact, the BioXen system must be deployed as an open-source platform, including full documentation of algorithm implementations and parameters. Following the precedent set by successful biological analysis tools 6, encouraging the publication of the analysis code alongside derived results ensures maximum rigor and external validation, solidifying the system’s commitment to increasing the reproducibility of biological research.5

#### **Works cited**

1. Systems biology derived discoveries of intrinsic clocks \- Frontiers, accessed October 1, 2025, [https://www.frontiersin.org/journals/neurology/articles/10.3389/fneur.2017.00025/full](https://www.frontiersin.org/journals/neurology/articles/10.3389/fneur.2017.00025/full)  
2. Overview of Circadian Rhythms \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC6707128/](https://pmc.ncbi.nlm.nih.gov/articles/PMC6707128/)  
3. Control Theory Meets Synthetic Biology \- MIT, accessed October 1, 2025, [http://web.mit.edu/ddv/www/papers/Paperddv\_v5.pdf](http://web.mit.edu/ddv/www/papers/Paperddv_v5.pdf)  
4. MIMO Model Identification — Dynamic Optimization \- APMonitor, accessed October 1, 2025, [https://apmonitor.com/do/index.php/Main/ModelIdentification](https://apmonitor.com/do/index.php/Main/ModelIdentification)  
5. Guidelines for Genome-Scale Analysis of Biological Rhythms \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC5692188/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5692188/)  
6. Rhythmidia: A modern tool for circadian period analysis of filamentous fungi | PLOS Computational Biology \- Research journals, accessed October 1, 2025, [https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1012167](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1012167)  
7. Rhythmidia: A modern tool for circadian period analysis of filamentous fungi \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC11326708/](https://pmc.ncbi.nlm.nih.gov/articles/PMC11326708/)  
8. Rhythmidia: A modern tool for circadian period analysis of filamentous fungi \- PubMed, accessed October 1, 2025, [https://pubmed.ncbi.nlm.nih.gov/39102446/](https://pubmed.ncbi.nlm.nih.gov/39102446/)  
9. Design and Analysis of Large-Scale Biological Rhythm Studies: A Comparison of Algorithms for Detecting Periodic Signals in Biological Data \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/256931731\_Design\_and\_Analysis\_of\_Large-Scale\_Biological\_Rhythm\_Studies\_A\_Comparison\_of\_Algorithms\_for\_Detecting\_Periodic\_Signals\_in\_Biological\_Data](https://www.researchgate.net/publication/256931731_Design_and_Analysis_of_Large-Scale_Biological_Rhythm_Studies_A_Comparison_of_Algorithms_for_Detecting_Periodic_Signals_in_Biological_Data)  
10. MetaCycle: an integrated R package to evaluate periodicity in large scale data \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC5079475/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5079475/)  
11. Searching for Biological Rhythms: Peak Detection in the Periodogram of Unequally Spaced Data, accessed October 1, 2025, [https://www.euroestech.net/resources/VanDongen\_1999.pdf](https://www.euroestech.net/resources/VanDongen_1999.pdf)  
12. \[0901.2573\] The generalised Lomb-Scargle periodogram. A new formalism for the floating-mean and Keplerian periodograms \- arXiv, accessed October 1, 2025, [https://arxiv.org/abs/0901.2573](https://arxiv.org/abs/0901.2573)  
13. Basic Methods of Cell Cycle Analysis \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9963451/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9963451/)  
14. (PDF) Wavelet Analysis: Mother Wavelet Selection Methods \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/259810533\_Wavelet\_Analysis\_Mother\_Wavelet\_Selection\_Methods](https://www.researchgate.net/publication/259810533_Wavelet_Analysis_Mother_Wavelet_Selection_Methods)  
15. Wavelet Families \- MATLAB & Simulink \- MathWorks, accessed October 1, 2025, [https://www.mathworks.com/help/wavelet/ug/wavelet-families-additional-discussion.html](https://www.mathworks.com/help/wavelet/ug/wavelet-families-additional-discussion.html)  
16. Optimal Wavelet Selection for Signal Denoising \- PMC \- National Institutes of Health (NIH) |, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC11486496/](https://pmc.ncbi.nlm.nih.gov/articles/PMC11486496/)  
17. synergetics/spectrum: Higher Order Spectrum Estimation toolkit \- GitHub, accessed October 1, 2025, [https://github.com/synergetics/spectrum](https://github.com/synergetics/spectrum)  
18. Consensus Error Performance of Linear Multi-Agent Systems | Request PDF, accessed October 1, 2025, [https://www.researchgate.net/publication/367010696\_Consensus\_Error\_Performance\_of\_Linear\_Multi-Agent\_Systems](https://www.researchgate.net/publication/367010696_Consensus_Error_Performance_of_Linear_Multi-Agent_Systems)  
19. Rhythmic expression of \- Dataset \- Catalog \- Data.gov, accessed October 1, 2025, [https://catalog.data.gov/dataset/rhythmic-expression-of](https://catalog.data.gov/dataset/rhythmic-expression-of)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAYAAACtWK6eAAAAsUlEQVR4Xu3BAQEAAACCIP+vbkhAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAB8GXHmAAEdo+NeAAAAAElFTkSuQmCC>