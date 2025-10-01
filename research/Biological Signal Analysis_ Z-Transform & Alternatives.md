

# **A Comprehensive Literature Review on Z-Transforms, Limitations, and Advanced Alternative Methodologies for Frequency Domain Analysis in Biological Systems**

## **I. Foundational Principles of Discrete System Analysis via the Z-Transform**

The analysis of sampled biological signals and the design of digital controllers for bioengineering applications fundamentally rely on mathematical tools capable of translating time-domain information into the frequency or complex-frequency domain. The Z-transform serves as the primary analytical instrument for discrete-time systems, establishing a necessary complex-plane framework.1

### **A. Definition, Derivation, and Relationship to Continuous Transforms**

The Z-transform, denoted ![][image1], fundamentally links the discrete time domain sequence ![][image1] to the complex ![][image1]\-domain via the definition:  
![][image1]This formulation of the Z-transform is the direct counterpart to the Laplace transform used for continuous-time signals.1 More critically, the Z-transform is recognized as a generalization of the Discrete-Time Fourier Transform (DTFT). The principal motivation for this generalization stems from the fact that the Fourier transform does not converge for all sequences, thereby limiting the class of signals amenable to analysis.1 By introducing the complex variable  
![][image1], the scope of transformable signals is significantly broadened through the Region of Convergence (ROC).  
The derivation of the Z-transform often proceeds from the Laplace transform by defining a new complex variable, ![][image1], and associating it with the ![][image1]\-variable using the definition ![][image1].2 This definition allows complex variable theory to be applied to problems involving discrete time signals and systems, simplifying otherwise intractable time-domain manipulations.1 The specific use of  
![][image1] rather than ![][image1] in the summation and the defined relationship between ![][image1] and the parameters ![][image1] and ![][image1] are intentional choices optimized for digital signal processing (DSP). This convention is specifically designed to provide the simplest algebraic means of moving between the system's recursive filter coefficients (time-domain implementation) and its ![][image1]\-domain transfer function representation.2 This emphasis on efficient implementation dictates the LTI framework, which can sometimes impose analytical restrictions when modeling non-linear physical phenomena.

### **B. Core Properties and LTI System Representation**

The Z-transform enables powerful algebraic analysis of Linear Time-Invariant (LTI) systems. A discrete-time LTI system is defined by the convolution sum, ![][image1] 1, where  
![][image1] is the impulse response. A defining advantage of the Z-transform is its ability to simplify this convolution sum into algebraic multiplication in the ![][image1]\-domain: ![][image1], where ![][image1] is the system’s transfer function.  
The time-shifting (or delay) property is paramount in control design. A signal ![][image1] that is simply a delayed version of ![][image1] (e.g., ![][image1]) translates into the ![][image1]\-domain as ![][image1].3 This facilitates the analysis and compensation of propagation delays common in digital biosensors or biocontrol loops. For instance, if the time domain signal  
![][image1] is known, the delayed signal ![][image1] can be precisely derived using this property.3  
Crucially, the transfer function analysis, similar to its continuous-time Laplace counterpart, relies on the Z-transform of the unit impulse function being unity.4 This allows techniques like pole-zero stability analysis to be applied to discrete systems. Because the system's stability in the time domain is defined by the convergence of its impulse response  
![][image1] 1, if a complex biological model yields an unstable Z-domain transfer function (poles outside the unit circle), it indicates a critical failure in the underlying linear model or discretization process, highlighting the rigidity of the LTI constraint in a dynamic, closed-loop biological system.

## **II. Application of Z-Domain Analysis in Bioengineering and Biocontrol**

Despite its inherent constraints, the Z-transform remains indispensable in areas of bioengineering where the LTI approximation holds locally or where system control requires explicit discretization.

### **A. Biocontrol and Digital Biosensor Systems**

In digital control systems, the Z-transform is the standard methodology for designing digital feedback controllers.2 Bioreactor control loops, digital biosensors, and similar embedded systems use the Z-transform to convert continuous control theory into discrete difference equations implementable by microprocessors.  
The practical application of the Z-transform’s delay property is seen in describing signal propagation. For example, if a signal ![][image1] follows a pattern like ![][image1] times a unit step, a signal ![][image1] delayed by one time step will be defined as ![][image1] times a unit step delayed by one time step.3 Understanding and accurately modeling such delays using  
![][image1] in the complex domain is critical for maintaining stability in closed-loop systems, compensating for transport lag, and ensuring actuator timing is precise.  
The framework is also essential in discrete optimal control theory, which seeks to govern complex biological objectives, such as pest management. These problems often involve maximizing a "valuable" population while minimizing pest populations and the cost of control strategies.5 The process uses the extension of Pontryagin's maximum principle to discrete systems, which requires deriving adjoint systems and characterizing optimal controls over discrete time steps.5 Although the overall dynamics rely on complex non-linear models (e.g., population dynamics), the Z-transform and the discrete framework it supports are instrumental for structuring the control computation and calculating optimal actions step-by-step. The transformation serves primarily as an efficient computational architecture for implementing complex optimization, rather than a robust method for analyzing the underlying, potentially non-linear biological dynamics.

### **B. Analysis of Sampled Physiological Signals**

In neuroscience, the Z-transform concept can be adapted for modeling sampled physiological responses like neuronal spike trains. When sampled at a sufficiently high rate, spike trains yield binary responses (spike or no-spike per sample interval ![][image1]).6 Analysis often involves determining the conditional histogram  
![][image1], which relates stimulus parameters to the probability of spiking.  
However, the application of Z-domain tools in this domain immediately exposes their limitations. Conditional distributions in neurobiology are generally **not Gaussian**.6 Furthermore, data sparsity often results in under-sampled tails of these distributions. To manage this deviation from ideal assumptions, researchers must employ secondary, non-parametric techniques, such as applying a smoothing spline, or fit the non-linearity using an external parametric model.6 This necessity for statistical "escape hatches" confirms that the classical LTI framework of the Z-transform is mathematically insufficient for inherently stochastic, real-world biological randomness, forcing reliance on statistical adjustments rather than inherent analytical power.

## **III. Theoretical and Operational Limitations of Z-Transform in Biological Systems**

The primary drawback of the Z-transform stems from its fundamental requirement for the system under analysis to be Linear and Time-Invariant (LTI). This assumption is broadly violated by the inherent complexity, scale, and time-varying nature of living systems.

### **A. The Critical Challenge of Non-Linearity**

Biological dynamics are defined by non-linear relationships, rendering the Z-transform's assumption of linearity fundamentally problematic. A classic example is enzyme kinetics, which follows **Michaelis–Menten kinetics**.7 The reaction rate  
![][image1] is a non-linear function of substrate concentration ![][image1], defined by the differential equation ![][image1].7 Because the Z-transform (and the transfer functions it produces) cannot directly analyze systems defined by such ratios and non-linear dependencies, its application requires heavy local linearization, which often sacrifices significant modeling fidelity.  
When this non-linearity is combined with stochasticity, the deficiencies multiply. The conditional distributions of biological signals, such as neuronal responses, are often non-Gaussian.6 Attempting to map these non-linear, non-Gaussian processes onto a linear framework optimized for analytical algebraic solutions means that the modeler must perform a critical choice: either severely simplify the biological process (sacrificing accurate representation) or use the Z-transform only as an algebraic tool for a highly restricted linear component, while treating the non-linear or statistical aspects separately, for instance, by smoothing the data distribution.6 This necessitates a modeling triage where the Z-transform is relegated to a supportive, computational role rather than the primary method for dynamic analysis.

### **B. Inadequacy for Complexity and Scale (MIMO Systems)**

Beyond non-linearity, the scale and connectivity of biological systems pose an organizational challenge for Z-domain analysis. The classical Z-transform approach yields a transfer function (TF) representation, ![][image1], which is primarily suited for **Single-Input, Single-Output (SISO) systems**.8  
Biological regulatory networks—be they gene expression pathways, metabolic cycles, or coupled physiological control systems—are inherently **Multiple-Input, Multiple-Output (MIMO)** systems. These systems involve dozens or hundreds of coupled variables, complex feedback loops, and parallel regulatory paths. While a transfer function description can be theoretically derived for MIMO systems using matrix representations, the resulting polynomial ratios for high-order, coupled systems become analytically unwieldy and impractical for pole-zero analysis.8 The inability of the TF framework to effectively manage these large, interconnected systems limits the utility of the Z-transform in holistic systems biology.

### **C. Computational and Real-Time Operational Constraints**

In bioengineering, particularly real-time control applications, computational complexity is a major limitation. The implementation of frequency analysis derived from the Z-transform, often through the Discrete Fourier Transform (DFT) accelerated by the Fast Fourier Transform (FFT) algorithm 9, can impose significant operational burdens.  
In applications requiring high-rate data telemetry, such as real-time vibration analysis or high-frequency biosensing, the sheer volume of data samples coupled with the computational effort of conventional FFT algorithms places a significant demand on bandwidth and processing power.9  
Furthermore, in bioprocess control, simplicity and computational efficiency are often paramount. While complex closed-loop control (CLC) is necessary to adjust continuously based on real-time output and achieve low error, the easier open-loop control (OLC), which lacks this continuous corrective feature, results in substantially higher error accumulation.10 The search for control techniques that maintain the precision of CLC while reducing complexity has driven researchers away from classic Z-domain analysis toward alternatives. This operational imperative has prioritized pragmatic solutions, such as algebraic control combined with Fourier series, specifically because they reduce mathematical complexity and computational effort while still yielding continuous control profiles suitable for practical application in fields like bioethanol production.10 This demonstrates that operational efficiency, rather than pure theoretical analysis, often dictates the choice of modeling framework in industrial bioengineering.

## **IV. Advanced Time-Frequency and Decomposition Alternatives**

To effectively analyze the non-stationary and non-linear characteristics pervasive in biological data, methods that offer time-frequency localization are necessary, directly addressing the limitations of the Z-transform's global frequency perspective.

### **A. Wavelet Transforms (WT)**

The Z-transform, particularly when evaluated on the unit circle (DTFT), provides a global assessment of frequency content across the entire duration of the signal, meaning it assumes stationarity. Biological signals, such as electromyography (EMG) or electroencephalography (EEG), are highly non-stationary, characterized by transient events, localized changes in frequency content, and varying spectral characteristics over time.  
The Wavelet Transform (WT) overcomes this fundamental limitation by providing superior **time-frequency localization**. Unlike the Z-transform, WT allows for simultaneous analysis of a signal’s energy distribution in both the time and frequency domains, making it highly effective for analyzing transients and non-periodic phenomena. The Discrete Wavelet Transform (DWT) is widely used for signal processing tasks in biology, including noise reduction and feature extraction.11 Comparative studies in fields like EMG signal classification confirm that DWT is a powerful tool for capturing the localized features necessary for clinical diagnosis and pattern recognition, demonstrating its superiority over fixed-basis transforms when analyzing dynamic physiological responses.11 The shift towards Wavelets is an explicit acknowledgment that the fundamental nature of physiological data is non-stationary, rendering global frequency transforms inadequate for accurate signal characterization.

### **B. Empirical Mode Decomposition (EMD) and Hilbert-Huang Transform (HHT)**

For signals where the underlying oscillatory components are complex and entirely unknown, the Empirical Mode Decomposition (EMD) technique provides an adaptive, data-driven alternative. EMD decomposes a non-stationary signal into a set of basis functions, known as Intrinsic Mode Functions (IMFs), which are derived directly from the data itself.  
EMD has proven useful in analyzing specific biological signals, such as the steady-state visual evoked potential (SSVEP).12 This method adapts to time-varying characteristics without requiring  
*a priori* definitions of basis functions. However, this high degree of adaptivity comes with constraints. Research has shown that while EMD is effective for limited stimulation frequency ranges, extending this operational range seriously challenges the methodology. This necessitates complex post-processing, often involving the combination of multiple IMFs, which may introduce error into the final analysis.12 This sensitivity highlights a crucial trade-off: highly adaptive, data-driven methods often lack the inherent mathematical robustness and predictable decomposition properties guaranteed by fixed-basis transforms like the Z-transform. This forces system validation to be highly domain-specific.

### **C. Other Time-Series and Statistical Methods**

The analysis of complex biological data often moves entirely outside the realm of frequency transforms into specialized time-series statistical modeling. High-throughput data, such as developmental microarray time course data, requires specialized statistical analysis and graphical display functions.13 Computational resources like the Bioconductor project provide packages specifically tuned for these biological time-series analyses.13 These methods focus on tracking changes, differential expression, and correlation over time, providing statistical inference that cannot be achieved via classical frequency domain transformation alone.

## **V. Alternative Architectures for Complex Biological System Control and Modeling**

For controlling and modeling complex, uncertain, and high-dimensional biological systems, the field has largely migrated from the input-output focus of the Z-transform transfer function to structured architectural frameworks.

### **A. State-Space Modeling: The MIMO Solution**

The most significant architectural alternative to the Z-domain transfer function is the State-Space model. State-Space modeling represents a system using a set of first-order differential or difference equations that describe the evolution of internal state variables (![][image1]) over time, driven by inputs (![][image1]) and mapped to outputs (![][image1]). This model is explicitly preferred because it overcomes the structural limitations of transfer functions, which are primarily SISO-focused.8 State-Space models are inherently capable of handling  
**Multiple-Input, Multiple-Output (MIMO) systems** and are recognized for their versatility in modeling complex biological phenomena.8  
The transition from a Z-transform (external input/output description) to a State-Space model (internal state representation) signifies a fundamental philosophical shift in bioengineering. Instead of merely describing how system inputs map to outputs, the State-Space model provides direct insight into the internal physics and coupling of the system via its state variables (e.g., specific cell concentrations, internal metabolite levels, or neuronal firing states). This capability is essential for synthetic biology and bioreactor design, where precise monitoring and control of intermediate, internal variables is necessary for robust system operation.

### **B. Advanced and Adaptive Control Strategies**

When biological variability is high, or system dynamics are unknown, fixed-parameter controllers derived from the Z-transform are inadequate.

#### **Model-Reference Adaptive Control (MRAC)**

Model-Reference Adaptive Control (MRAC) is designed specifically to regulate a system of interest (the "plant") whose dynamics are largely unknown.14 This architecture uses adaptive feedback to ensure that the unknown system behaves identically to a known, well-characterized reference model.14 By using an online adaptive mechanism, MRAC implicitly addresses the pervasive problem of  
**parameter uncertainty** and model mismatch inherent in biological systems (e.g., batch-to-batch variation in cell cultures or inter-patient variability). This approach grants superior robustness against high biological variability compared to classical control systems derived from fixed Z-domain transfer functions.

#### **Discrete Optimal Control Theory**

For non-linear, constrained systems, discrete optimal control theory provides a powerful, rigorous framework. By applying the discrete version of Pontryagin's maximum principle, optimal control strategies can be characterized for resource management and dynamic regulation.5 This framework, when applied to problems such as integrated pesticide and biological pest control, dictates the optimal timing and magnitude of intervention, operating far beyond the scope of simple linear feedback control.5

#### **Algebraic Control for Non-Linear Bioprocesses**

To specifically address the challenge of real-time control complexity, novel algebraic methods combined with Fourier series have been proposed. This methodology has demonstrated effectiveness in addressing complex, non-linear dynamic optimization problems in bioprocesses.10 The objective of this approach is to reduce mathematical complexity and computational effort while simultaneously producing continuous control profiles suitable for practical industrial application.10 This trend towards computational simplification is crucial in bioengineering, where real-time implementation often dictates the feasibility of a control strategy.

## **VI. Synthesis and Future Directions**

The Z-transform remains a cornerstone for digital filter design and the conceptual analysis of discrete LTI components. However, its utility as the primary tool for holistic biological system modeling and frequency analysis is severely limited by the necessity of LTI assumptions and the complexity of real-world biological data.

### **A. Comparative Summary of Modeling Paradigms**

A direct comparison illustrates how alternative methodologies compensate for the analytical deficiencies of the Z-transform:  
Table 1: Comparison of Frequency/Time-Frequency Analysis Techniques for Bio-Signals

| Method | Domain Focus | Primary Suitability (LTI/Non-Linear) | Key Computational Constraint | Typical Biological Application |
| :---- | :---- | :---- | :---- | :---- |
| Z-Transform (TF) | Discrete Frequency (![][image1]\-plane) | Strict LTI Systems, SISO Control | Requires analytical solution of difference equations | Digital filter design, simple control loop analysis 3 |
| Discrete Fourier Transform (FFT) | Global Frequency Spectrum | Stationary, Periodic Signals | High computational load for real-time, high-rate data 9 | Spectral power estimation, steady-state analysis |
| Discrete Wavelet Transform (DWT) | Time-Frequency Localization | Non-Stationary Signals, Transients | Moderate, requires selection of appropriate mother wavelet | EMG classification, feature extraction 11 |
| Empirical Mode Decomposition (EMD) | Time Domain (Intrinsic Modes) | Highly Non-Stationary, Non-Linear, Adaptive | Highly sensitive to noise and frequency range extension 12 | SSVEP decomposition, artifact removal |

For control architecture, the contrast between the input-output model of the transfer function and the descriptive internal model of state-space methods is clear:  
Table 2: Transfer Function vs. State-Space Modeling in Biocontrol

| Modeling Paradigm | Primary Mathematical Representation | System Complexity Capacity | Key Advantages | Limitation Addressed (from Z-TF) |
| :---- | :---- | :---- | :---- | :---- |
| Transfer Function (![][image1]\-Domain) | Ratio of polynomials in ![][image1] | Single-Input, Single-Output (SISO) | Algebraic simplicity, classical root locus analysis | Limited to LTI systems; poor handling of internal dynamics |
| State-Space Model | System matrices (A, B, C, D) | Multiple-Input, Multiple-Output (MIMO) 8 | Versatility, direct insight into internal states, handles time-varying systems | Overcomes inherent MIMO limitation of TFs 8 |
| Adaptive Control (MRAC) | Multiple dynamic models (Plant, Reference, Adaptation Law) | Unknown/Time-Varying Systems | High robustness against model uncertainty and parameter drift 14 | Eliminates the need for precise, fixed LTI model identification |

### **B. The Trajectory Towards Data-Driven Hybrid Modeling**

The trajectory of advanced signal processing and biocontrol points toward the dominance of methods that specifically manage non-linearity, non-stationarity, and high system dimensionality. The analytical community has moved from focusing on methods that simplify algebraic manipulation (Z-transform) to methods that achieve robust representation of complex dynamics (State-Space) and accurate localization of time-varying features (Wavelets, EMD).  
The continued focus on reducing mathematical and computational complexity, such as the use of algebraic control combined with Fourier analysis 10, confirms that real-time implementation constraints remain a major driver of model selection in bioengineering. Future research is concentrating on hybrid models that integrate localized analysis techniques (e.g., DWT 11) with robust control architectures (e.g., MRAC 14). Furthermore, emerging methods leveraging machine learning and deep neural networks are increasingly being used to directly map complex, non-linear, and uncertain biological inputs to outputs, potentially circumventing the need for classical analytical transforms altogether in pattern recognition and predictive modeling tasks.  
The Z-transform, while historically significant, is now primarily a tool for structuring discrete-time calculations rather than the defining method for understanding the intrinsic, dynamic, and non-linear reality of biological systems.

#### **Works cited**

1. Transform Domain Representation of Discrete Time Signals The Z Transform, accessed October 1, 2025, [https://web.ece.ucsb.edu/\~yoga/courses/DSP/P6\_Z\_Transform.pdf](https://web.ece.ucsb.edu/~yoga/courses/DSP/P6_Z_Transform.pdf)  
2. The Scientist and Engineer's Guide to Digital Signal Processing The z-Transform \- Analog Devices, accessed October 1, 2025, [https://www.analog.com/media/en/technical-documentation/dsp-book/dsp\_book\_ch33.pdf](https://www.analog.com/media/en/technical-documentation/dsp-book/dsp_book_ch33.pdf)  
3. Digital control 3: The Z-transform \- YouTube, accessed October 1, 2025, [https://www.youtube.com/watch?v=NtYne9Nnsi8](https://www.youtube.com/watch?v=NtYne9Nnsi8)  
4. The Z Transform \- Linear Physical Systems Analysis, accessed October 1, 2025, [https://lpsa.swarthmore.edu/ZXform/FwdZXform/FwdZXform.html](https://lpsa.swarthmore.edu/ZXform/FwdZXform/FwdZXform.html)  
5. Discrete Time Optimal Control Applied to Pest Control Problems \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/262765920\_Discrete\_Time\_Optimal\_Control\_Applied\_to\_Pest\_Control\_Problems](https://www.researchgate.net/publication/262765920_Discrete_Time_Optimal_Control_Applied_to_Pest_Control_Problems)  
6. Analysis of Neuronal Spike Trains, Deconstructed \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC4970242/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4970242/)  
7. Michaelis–Menten kinetics \- Wikipedia, accessed October 1, 2025, [https://en.wikipedia.org/wiki/Michaelis%E2%80%93Menten\_kinetics](https://en.wikipedia.org/wiki/Michaelis%E2%80%93Menten_kinetics)  
8. accessed October 1, 2025, [https://kamman-dynamics-control.org/wp-content/uploads/2021/01/51-me360state-space-models-and-transfer-functions-1.pdf](https://kamman-dynamics-control.org/wp-content/uploads/2021/01/51-me360state-space-models-and-transfer-functions-1.pdf)  
9. A Review of FFT Algorithms and A Real-Time Algorithm Development for Airborne Vibration Testing Applications \- AMA Science, accessed October 1, 2025, [https://www.ama-science.org/proceedings/download/AGplAD==](https://www.ama-science.org/proceedings/download/AGplAD==)  
10. Fourier Optimization and Linear-Algebra-Based Combination of Controls to Improve Bioethanol Production \- MDPI, accessed October 1, 2025, [https://www.mdpi.com/2227-9717/13/9/2792](https://www.mdpi.com/2227-9717/13/9/2792)  
11. A comparative study of wavelet families for electromyography signal classification based on discrete wavelet transform | Request PDF \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/343866889\_A\_comparative\_study\_of\_wavelet\_families\_for\_electromyography\_signal\_classification\_based\_on\_discrete\_wavelet\_transform](https://www.researchgate.net/publication/343866889_A_comparative_study_of_wavelet_families_for_electromyography_signal_classification_based_on_discrete_wavelet_transform)  
12. The Empirical Mode Decomposition-Decision Tree Method to Recognize the Steady-State Visual Evoked Potentials with Wide Frequency Range \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC6293644/](https://pmc.ncbi.nlm.nih.gov/articles/PMC6293644/)  
13. timecourse \- Bioconductor, accessed October 1, 2025, [https://bioconductor.org/packages/release/bioc/html/timecourse.html](https://bioconductor.org/packages/release/bioc/html/timecourse.html)  
14. Biological Interpretation of Model-Reference Adaptive Control in a Mass Action Kinetics Metabolic Pathway Model \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC5859569/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5859569/)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAYAAACtWK6eAAAAsUlEQVR4Xu3BAQEAAACCIP+vbkhAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAB8GXHmAAEdo+NeAAAAAElFTkSuQmCC>