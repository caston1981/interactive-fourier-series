

# **The Frequency Domain in Biological Systems Analysis: A Foundational Review of Fourier and Laplace Transforms**

## **Introduction: The Necessity of Frequency Domain Methods in Biological Dynamics**

The analysis of biological systems, ranging from molecular kinetics to organismal physiology, presents unique challenges rooted in the inherently dynamic, stochastic, and coupled nature of living processes. Traditional analysis in the time domain, often relying on coupled rate equations, frequently fails to capture essential system properties such as stability, frequency response, robustness to perturbations, and inherent rhythmicity. The application of classical signal processing and control theory, particularly through the use of the Fourier Transform (FT) and the Laplace Transform (LT), provides a necessary and powerful abstraction layer to analyze these complex dynamics.

### **Biological Signals as Dynamic Systems: Rhythms, Noise, and Control**

Biological signals are fundamentally oscillatory. The ubiquity of rhythmicity necessitates Fourier methods for decomposition and identification. At the systemic level, fundamental biological clocks, most notably the circadian system, impose approximately 24-hour periodicities on nearly all physiological and behavioral processes.1 The rigorous characterization of these rhythms demands analysis techniques capable of isolating specific frequencies from complex, noisy time series.  
Similarly, the organization of neural activity is predominantly oscillatory. Electroencephalography (EEG), magnetoencephalography (MEG), and local field potential (LFP) recordings show clear oscillations classified by frequency bands (e.g., delta, theta, alpha/mu, beta, gamma).3 The study of these neural phenomena is critically dependent on spectral analysis, which transforms the time-domain signal into its component frequencies, providing critical insight into brain state, cognition, and connectivity.4 Biomedical Signal Processing (BSP) confirms that time and frequency domain analyses are vital methodologies for interpreting these physiological signals, which are crucial for diagnostics and health monitoring.7  
Modern computational and synthetic biology leverages frequency domain techniques to treat genetic and metabolic circuitry as engineered systems. Control theory, which relies on the Laplace Transform, enables the formal analysis of dynamic behavior. This approach provides the tools necessary to rigorously assess feedback loops, predict stability, and measure robustness against parametric uncertainty and environmental disturbances.8

### **The Universal Applicability of Control Principles**

A key observation arising from the successful application of engineering mathematics to biology is the striking parallel between optimally designed engineered control devices and naturally evolved biological systems. Research suggests an element of "convergent evolution" between complex artificial devices and biological systems.10 This convergence implies that natural selection optimized stability and robustness mechanisms (e.g., homeostasis, highly stable genetic clocks) using strategies that adhere to the same underlying physical and control principles formalized in classical engineering mathematics. Thus, the FT and LT are not merely analytical tools but mathematical representations of universal design constraints that govern both living and man-made dynamic systems.  
However, the powerful predictive capacity of the Laplace Transform is primarily rooted in its application to Linear Time-Invariant (LTI) systems. Biological systems are fundamentally nonlinear; therefore, applying the LT rigorously requires linearization of the nonlinear ordinary differential equations (ODEs) around a steady-state equilibrium point.11 The predictive success of the subsequent control analysis hinges entirely on the validity and relevance of this linearization step. While the LTI approximation is highly effective for assessing local behavior, such as robustness to small perturbations or basal noise, it may not adequately predict global behaviors like large-scale switching, bistability, or complex nonlinear dynamics, which often require dedicated nonlinear analysis methods.  
---

## **Section 1: Fourier Transform Applications in Biological Signal Decomposition**

The Fourier Transform (![][image1]) maps a signal from the time domain ![][image1] to the frequency domain ![][image1], decomposing the signal into its constituent sinusoidal frequencies. This transformation is central to identifying periodic components, analyzing signal structure, and diagnosing rhythmic activity across multiple scales in biology.

### **1.1. Fourier Analysis in Temporal Omics and Circadian Rhythms**

Frequency analysis is indispensable for detecting rhythmicity in high-dimensional omics datasets (transcriptomics, proteomics, metabolomics) derived from time-series experiments. A major challenge in these experiments is the practical impossibility of achieving perfectly uniform, complete sampling. Biological time-series data often contain missing points or are sampled irregularly, rendering the standard Discrete Fourier Transform (DFT) unreliable due to issues like spectral leakage and aliasing.12

#### **The Lomb-Scargle Periodogram (LSP)**

The recognized solution for spectral analysis of unevenly or sparsely sampled biological data is the **Lomb-Scargle Periodogram (LSP)**.14 Originating from astronomy and signal processing, the LSP works by evaluating the goodness-of-fit of a sinusoidal model across a range of candidate frequencies using a least-squares approach, effectively sidestepping the uniform sampling requirement of the standard DFT.12 Research demonstrates that the LSP exhibits superior detection efficiency and accuracy when analyzing noisy data and, crucially, avoids the bias or erroneous results that can arise from interpolating missing data points.12 This makes the LSP the appropriate mathematical tool for analyzing observational time series obtained from free-living systems, such as telemetrical data from animals.12

#### **Integrative Tools and Reliability Engineering**

Modern circadian transcriptomics relies on integrative computational packages to manage the heterogeneity inherent in biological data. The **MetaCycle** R package is a notable example, designed to overcome the individual weaknesses of specific rhythm-detection algorithms by incorporating and integrating the results of three distinct methods 13:

1. **Lomb-Scargle (LS):** A signal processing method ideal for irregular sampling.  
2. **JTK\_CYCLE (Jonckheere-Terpstra-Kendall):** A statistical, non-parametric method based on rank correlation, providing robustness against non-sinusoidal shapes and noise.13  
3. **ARSER (Autoregressive Spectral Estimation):** A computer science technique based on autoregressive models, which typically requires complete and evenly sampled data but is efficient for high-quality datasets.13

The methodology employed by MetaCycle’s meta2d function, which integrates results based on combining *P*\-values, period length, and phase from these disparate algorithms 13, is an application of N-version programming (NVP)—a redundancy strategy borrowed from reliability engineering. This strategic integration of methods from computer science, statistics, and physics significantly enhances the robustness and reliability of rhythm detection in large-scale biological data, underscoring the necessity for methodological fault tolerance when dealing with inherently complex, noisy biological measurements.  
Table 1 provides a functional comparison of the key periodicity detection algorithms integrated within high-throughput omics analyses.  
Table 1: Comparison of Frequency-Domain Methods in Circadian Transcriptomics

| Algorithm | Domain/Discipline | Core Mathematical Basis | Data Requirement | Advantage |
| :---- | :---- | :---- | :---- | :---- |
| ARSER | Computer Science/Statistics | Autoregressive models, Spectral Density | Evenly sampled/Complete 13 | Efficient for large, clean datasets |
| JTK\_CYCLE | Non-parametric Statistics | Rank-based non-parametric test | Handles noise/low sampling 13 | Robust to non-sinusoidal shapes and outliers |
| Lomb-Scargle Periodogram (LSP) | Physics/Signal Processing | Least-squares fit of sinusoids | Unevenly/Sparsely sampled 12 | Avoids bias/error from interpolation of missing data 12 |

### **1.2. Fourier Analysis in Structural Biology and Imaging**

The determination of three-dimensional atomic structures, particularly through X-ray crystallography, represents perhaps the most profound and foundational application of the Fourier Transform in structural biology. The relationship between the crystal structure and the measured diffraction pattern is mathematically defined by the Fourier transform pair.19

#### **The Fundamental Theorem of Crystallography**

In crystallography, the **electron density distribution** ![][image1] in the unit cell (real space) is a periodic function. It can be represented as a Fourier series, where the coefficients of the series are the **structure factors** ![][image1] (reciprocal space). The diffraction pattern measured experimentally provides the intensity ![][image1], which is proportional to the square of the magnitude of the structure factors (![][image1]). This relationship is summarized by the transform equations 20:  
![][image1]![][image1]  
The difficulty in structure determination, known as the "phase problem," stems from the fact that while the amplitude ∣Fhkl​∣ is directly measured, the phase information necessary to perform the inverse transform and reconstruct ρ(x,y,z) is lost during the measurement process. Overcoming this phase barrier constitutes a century-old challenge in the field.21

### **1.3. Fourier Analysis in Neural Dynamics and Electrophysiology (EEG/MEG)**

Spectral analysis is the cornerstone technique for characterizing the oscillatory components of neural time series.4 Transforming data into the frequency domain allows neuroscientists to identify frequency-specific phenomena associated with cognition, behavior, and neural connectivity. In this domain, the signal is represented as a linear combination of oscillatory basis functions, optimally revealing components like gamma (high-frequency) and theta (low-frequency) rhythms.4  
Advanced methodologies recognize that physiological oscillations are often dynamic, transient, and rarely perfectly sinusoidal.22 Consequently, contemporary analyses must incorporate methods that account for key confounds. One critical consideration is the distinction between true oscillations and aperiodic activity, often characterized as "1/f noise" (a broadband spectral slope).22 Failure to properly model and remove this aperiodic background activity can lead to misinterpretation of the magnitude and frequency of oscillatory peaks. Furthermore, the transient nature (burstiness) of neural activity necessitates time-frequency methods (such as wavelets or short-time Fourier transforms) to accurately estimate power and phase without averaging away critical temporal details.22

### **1.4. Fourier Analysis in Metabolic and Cellular Oscillations**

Frequency analysis is crucial for characterizing the endogenous rhythms that drive cell function beyond the canonical circadian clock. Within cellular metabolism, oscillations can be rapid (ultradian) or slow (infradian).  
For example, the Dominant Oscillating Islet Model (DOM) integrates three interacting oscillatory components—electrical/calcium, glycolytic, and mitochondrial—to explain the complex bursting patterns observed in pancreatic islets.23 Frequency analysis is applied here to investigate the slow metabolic oscillations, particularly the slow glycolytic bursting mode, enabling researchers to decouple and analyze the interaction between the distinct fast (calcium-driven) and slow (glycolysis-driven) oscillatory dynamics.23  
Similarly, mapping metabolic oscillations during cell cycle progression requires Fourier-based approaches. Analysis of metabolomic data (e.g., liquid chromatography-high resolution mass spectrometry) across cell cycle phases (G1 and S/G2M) reveals that hundreds of metabolites oscillate in coordination with cell division.24 Frequency analysis is implicitly utilized to identify and determine the period and phase of these metabolic trajectories relative to the cell cycle period, confirming broad metabolic remodeling synchronized with cellular proliferation.24  
---

## **Section 2: Laplace Transform and Control Theory in Biomolecular Systems**

The Laplace Transform (![][image1]) is the cornerstone of classical control theory, providing a means to convert linear time-invariant (LTI) differential equations into algebraic equations in the complex frequency domain (![][image1]). This algebraic representation, embodied by the transfer function, enables powerful analysis of system stability, performance, and robustness.

### **2.1. The Laplace Transform and Linear Time-Invariant (LTI) Approximations**

Biomolecular systems, governed by coupled, nonlinear rate equations (e.g., mass action, Michaelis-Menten, Hill kinetics), must be approximated as LTI systems to leverage the LT framework. This process involves linearizing the nonlinear dynamics, ![][image1], around a known steady-state equilibrium point ![][image1].11 The resulting linearized dynamics are represented in state-space form (  
![][image1]), where ![][image1] is the deviation from equilibrium. This LTI approximation is a powerful simplification that allows researchers to apply frequency-domain tools to assess how the system responds to small perturbations, such as intrinsic noise or minor environmental fluctuations, near its basal operating point.11

### **2.2. Transfer Functions and Stability Analysis (Poles and Zeros)**

The primary mathematical output of the LT applied to a linearized system is the transfer function, ![][image1], which formally relates the Laplace transform of the output ![][image1] to the Laplace transform of the input ![][image1], typically assuming zero initial conditions.11 Transfer functions are fundamental for modular systems analysis, as they allow complex cascades and feedback loops to be mathematically interconnected simply by multiplication (series connections) or summation (parallel connections).11

#### **Stability via Pole Location**

The most critical feature of the transfer function ![][image1] is the location of its **poles**, which are the roots of the denominator polynomial. These poles are mathematically equivalent to the eigenvalues of the linearized system matrix ![][image1] and determine the system's inherent dynamic behavior.11

* A stable system requires all poles to reside in the **left half** of the complex ![][image1]\-plane (![][image1]), ensuring that any transient response decays over time.  
* If poles lie precisely on the **imaginary axis** (![][image1]), the system exhibits sustained oscillations, characteristic of genetic oscillators or stable limit cycles (e.g., the circadian clock).25  
* Poles located in the **right half** of the ![][image1]\-plane (![][image1]) indicate exponential instability, typical of positive feedback loops designed to act as biological switches.11

Control theory thus serves as a critical **design principle** in synthetic biology. To engineer a reliable function—such as an oscillator (Repressilator) or a robust homeostatic regulator—the synthetic biologist must strategically choose reaction kinetics and parameters such that the system's poles (eigenvalues) are placed in the specific complex plane locations dictated by control theory.25

#### **The Del Vecchio & Murray Framework**

The rigorous application of control theory to biomolecular systems is extensively detailed in the seminal text, *Biomolecular Feedback Systems* by Del Vecchio and Murray.11 This framework utilizes transfer functions to dissect complex cellular interactions, particularly focusing on the analysis of feedback, robustness, and modularity.27 Transfer functions provide the necessary machinery to quantify  
**retroactivity**—the phenomenon where the performance of an upstream genetic module is severely degraded by the "loading" effect of a downstream module, causing a breakdown in modularity.27 Furthermore, frequency-domain representations derived from the LT (Bode plots, Nyquist plots) enable engineers to rigorously analyze loop stability and predict performance margins under varying feedback gains.  
Table 2: Mapping Laplace Domain Features to Biological System Properties

| Laplace Domain Feature | Definition | Biological Interpretation | Impact on System Dynamics |
| :---- | :---- | :---- | :---- |
| Transfer Function (![][image1]) | ![][image1] (Output LT / Input LT) | Input-output relationship of a biomolecular system or drug compartment 11 | Enables connection and analysis of modular circuits (cascade, feedback). |
| Poles (Roots of Denominator) | Eigenvalues of the Linearized System Matrix (![][image1]) 11 | Dictate the natural frequencies and stability of the system. | Left Half-Plane: Stability; Imaginary Axis: Sustained Oscillation; Right Half-Plane: Instability/Switching. |
| Zeros (Roots of Numerator) | Frequencies where system output is zero | Define frequencies that are attenuated or filtered by the system. | Crucial for designing noise rejection and signal robustness in genetic circuits.27 |

### **2.3. Pharmacokinetics/Pharmacodynamics (PK/PD) Modeling**

Compartmental models are the traditional means of describing drug absorption, distribution, metabolism, and excretion (ADME) in pharmacokinetics. These models simplify the body into one or more compartments (e.g., central plasma, highly perfused tissues, scarcely perfused tissues) and are inherently described by coupled linear ODEs.28  
The Laplace Transform offers an algebraically straightforward method for solving these compartmental models. An input dose is transformed (often as an impulse function, ![][image1]), and the complex PK model is represented by a transfer function ![][image1]. The concentration-time profile in plasma, ![][image1], is then the inverse Laplace transform of the product ![][image1]. This approach simplifies the estimation of PK parameters and allows analysts to rapidly simulate the effect of different dosing regimens.28 Furthermore, variations like the semi-compartmental model are used to link drug concentrations (PK) to observed effects (PD), accounting for phenomena like hysteresis without requiring full parameterization of the complex biological processes.29

### **2.4. Synthetic Biology: Designing Robust Feedback Control**

A primary motivation for applying control theory to synthetic biology is to enhance the performance and reliability of engineered genetic circuits against inherent cellular uncertainties, such as resource competition, intrinsic noise, and fluctuating plasmid copy numbers.8  
Negative feedback is mathematically proven to improve system robustness and disturbance rejection.32 The LT framework facilitates the formal design and implementation of high-gain feedback control strategies. For instance, synthetic circuits have been engineered using small RNAs (sRNAs) to create direct, closed-loop negative feedback that achieves more precise output tuning and improves robustness against noise compared to open-loop designs.32 Furthermore, sophisticated LT-based designs, such as integral control, are necessary to ensure that synthetic circuit output remains robustly at a precise steady-state setpoint despite continuous cellular resource fluctuations.30

#### **Optogenetics and In Silico Control**

Optogenetics provides an ideal physical layer for implementing advanced control systems because light inputs are high-bandwidth and precisely controllable in space and time.33 Researchers treat the cell containing the light-sensitive circuit as the control "plant." The required software controllers are designed  
*in silico*, often employing LTI models and transfer functions derived from system identification. This model-based approach enables the implementation of closed-loop control algorithms that use real-time measurements (e.g., fluorescence output) to automatically adjust the light input, thereby dynamically regulating gene expression to achieve a targeted biological outcome.34  
---

## **Section 3: Case Studies in Frequency Domain Problem Solving**

The following case studies demonstrate the utility and effectiveness of Fourier and Laplace methods in solving specific, high-impact biological and bioengineering problems.

### **3.1. Case Study: Laplace Transform in Population Genetics (Probabilistic Modeling)**

The Laplace Transform proves valuable beyond deterministic kinetics, serving as a powerful method for solving probabilistic problems in fields like population genetics.

* **Problem Solved:** Determining the time distribution of genetic coalescence—the process in which lineages within a sample trace back to a common ancestor. This analysis requires solving complex stochastic processes that are difficult to manage in the time domain.  
* **Method:** Graph-based algorithms for **Laplace transformed coalescence time distributions**.35  
* **Mechanism:** In queuing theory and coalescent theory, probability distributions in the time domain involve convolutions and differential equations. By applying the LT, the authors converted these complex time-domain relationships into algebraic expressions in the ![][image1]\-domain, greatly simplifying the computation of the expected distributions and moments.36 This capability allows for more efficient, open-source computational implementations of evolutionary modeling.  
* **Publication & Code:** Bisschop G (2022) Graph-based algorithms for Laplace transformed coalescence time distributions. **PLOS Computational Biology** 18(9): e1010532. DOI: 10.1371/journal.pcbi.1010532. The work constitutes a CAS-independent, open-source implementation.35

### **3.2. Case Study: Fourier Transform for Codon Periodicity in Genomics**

The Fourier Transform is a critical tool for computational genomics, specifically for *ab initio* gene prediction.

* **Problem Solved:** Identifying protein-coding regions within raw DNA sequences. Coding sequences inherently exhibit a repeating three-base pattern (codon) that is absent in non-coding DNA.  
* **Method:** **Fourier Transform (FT) analysis of numerically mapped DNA sequences**.37  
* **Mechanism:** DNA sequences are first converted into a numerical signal (e.g., via indicator functions where each base is mapped to a value). Applying the DFT to this signal reveals specific spectral components. The presence of a dominant peak in the power spectrum corresponding to a frequency of ![][image1] accurately indicates the three-base periodicity characteristic of an open reading frame, providing a robust, non-alignment-based method for gene prediction.39

### **3.3. Case Study: Integrated Periodicity Detection in Transcriptomics (MetaCycle)**

The inherent technical variability and noise in high-throughput biological data necessitate frequency analysis strategies that combine multiple methodological strengths.

* **Problem Solved:** Achieving robust, reliable detection of rhythmic gene expression in diverse, potentially noisy, and unevenly sampled circadian transcriptomics datasets.  
* **Method:** **MetaCycle R package**, utilizing N-version programming concepts to integrate the Lomb-Scargle Periodogram (LS), JTK\_CYCLE, and ARSER.13  
* **Mechanism:** By integrating the outputs of algorithms derived from fundamentally different disciplines (signal processing, statistics, and computer science), MetaCycle minimizes the risk of algorithm-specific failure modes. The LSP component ensures periodicity detection remains accurate even when data points are sparse or irregularly timed, a common limitation in *in vivo* experiments.13 This approach provides integrated statistical metrics (combined  
  *P*\-values, period, and phase) to yield high-confidence rhythm predictions.  
* **Publication & Code:** Wu, G., et al. (2016). MetaCycle: An integrated R package to evaluate periodicity in large scale data. **Bioinformatics** 32(18): 2854–2856. The package is available on CRAN and **GitHub**.13

### **3.4. Case Study: Closed-Loop Optogenetic Control of Gene Expression**

The Laplace Transform enables the transition from qualitative circuit modeling to quantitative biological engineering, especially when coupled with high-precision input hardware.

* **Problem Solved:** Achieving highly precise, dynamic, and computer-controlled regulation of target protein output within a living cell, compensating for cellular noise and resource limitations in real time.  
* **Method:** **Model-based design of a closed-loop optogenetic control system**.34  
* **Mechanism:** The system (e.g., the CcaR-CcaS optogenetic construct in *E. coli*) is first characterized using nonlinear kinetic models. These dynamics are linearized, and the Laplace Transform is used to derive the system's transfer function, providing a precise LTI model for the cellular "plant." This model is then used to design and tune a stabilizing feedback controller *in silico*. The controller uses real-time fluorescence output (measurement) to precisely modulate the light input (control signal), ensuring the protein level maintains a defined setpoint despite internal or external disturbances.34  
* **Publication & Code:** Lee, T. H. C., et al. (2021). Model-based design of a closed-loop optogenetic control system. *Analytical Chemistry* 93(8): 3833–3841. DOI: 10.1021/acs.analchem.0c04594. The approach relies on an explicit model-based design and control software.34

---

## **Conclusion**

Frequency domain analysis, leveraging the mathematical power of the Fourier and Laplace Transforms, provides essential tools for characterizing, designing, and optimizing dynamic biological systems. The Fourier Transform remains indispensable for decomposition and signal feature extraction, proving critical in fields ranging from structural determination (X-ray crystallography) to rhythm detection (circadian omics and neural oscillation analysis), particularly when paired with robust techniques like the Lomb-Scargle Periodogram to handle irregular sampling.  
The Laplace Transform anchors the field of systems and synthetic biology by enabling the application of rigorous classical control theory. By viewing biomolecular pathways as linear, time-invariant (LTI) systems near equilibrium, the transfer function methodology permits stability analysis (via pole placement), quantification of modularity challenges (retroactivity), and the formal design of robust feedback circuits. The universal principles of control revealed by the LT are not merely descriptive but serve as powerful **design blueprints**, guiding synthetic biologists in the engineering of reliable, predictable living systems, particularly in contexts like PK/PD modeling and advanced optogenetic control platforms.  
The future utility of frequency domain analysis in biology is expanding through the integration of these techniques into computational tools that specifically address the inherent complexity and noise of living matter, moving beyond simple modeling toward true biological engineering.

#### **Works cited**

1. Circadian Physiology | Roberto Refinetti PhD. \- Taylor & Francis eBooks, accessed October 1, 2025, [https://www.taylorfrancis.com/books/mono/10.1201/b19527/circadian-physiology-roberto-refinetti-phd](https://www.taylorfrancis.com/books/mono/10.1201/b19527/circadian-physiology-roberto-refinetti-phd)  
2. Circadian Physiology | Roberto Refinetti PhD. \- Taylor & Francis eBooks, accessed October 1, 2025, [https://www.taylorfrancis.com/books/mono/10.1201/9781420039016/circadian-physiology-roberto-refinetti-phd](https://www.taylorfrancis.com/books/mono/10.1201/9781420039016/circadian-physiology-roberto-refinetti-phd)  
3. High frequency oscillations in the intact brain \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC4895831/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4895831/)  
4. Analytical methods and experimental approaches for electrophysiological studies of brain oscillations \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC4007035/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4007035/)  
5. Rhythms of the Brain \- David Kleinfeld, accessed October 1, 2025, [https://neurophysics.ucsd.edu/courses/physics\_171/Buzsaki%20G.%20Rhythms%20of%20the%20brain.pdf](https://neurophysics.ucsd.edu/courses/physics_171/Buzsaki%20G.%20Rhythms%20of%20the%20brain.pdf)  
6. \[PDF\] Rhythms of the brain \- Semantic Scholar, accessed October 1, 2025, [https://www.semanticscholar.org/paper/Rhythms-of-the-brain-Buzs%C3%A1ki/7b10922cab71f51b1f08326d8cac1d8fa3bca685](https://www.semanticscholar.org/paper/Rhythms-of-the-brain-Buzs%C3%A1ki/7b10922cab71f51b1f08326d8cac1d8fa3bca685)  
7. Biomedical signal processing: A comprehensive overview \- International Journal of Research in Medical Science, accessed October 1, 2025, [https://www.medicalpaper.net/archives/2025/vol7issue1/PartB/7-1-19-674.pdf](https://www.medicalpaper.net/archives/2025/vol7issue1/PartB/7-1-19-674.pdf)  
8. Control theory meets synthetic biology \- PubMed, accessed October 1, 2025, [https://pubmed.ncbi.nlm.nih.gov/27440256/](https://pubmed.ncbi.nlm.nih.gov/27440256/)  
9. Control theory meets synthetic biology | Journal of The Royal Society Interface, accessed October 1, 2025, [https://royalsocietypublishing.org/doi/10.1098/rsif.2016.0380](https://royalsocietypublishing.org/doi/10.1098/rsif.2016.0380)  
10. Frequency domain analysis of noise in autoregulated gene circuits \- PNAS, accessed October 1, 2025, [https://www.pnas.org/doi/10.1073/pnas.0736140100](https://www.pnas.org/doi/10.1073/pnas.0736140100)  
11. Biomolecular Feedback Systems, accessed October 1, 2025, [https://www.cds.caltech.edu/\~murray/books/AM08/pdf/bfs-complete\_26May12.pdf](https://www.cds.caltech.edu/~murray/books/AM08/pdf/bfs-complete_26May12.pdf)  
12. The Lomb-Scargle Periodogram in Biological Rhythm Research: Analysis of Incomplete and Unequally Spaced Time-Series \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/245535651\_The\_Lomb-Scargle\_Periodogram\_in\_Biological\_Rhythm\_Research\_Analysis\_of\_Incomplete\_and\_Unequally\_Spaced\_Time-Series](https://www.researchgate.net/publication/245535651_The_Lomb-Scargle_Periodogram_in_Biological_Rhythm_Research_Analysis_of_Incomplete_and_Unequally_Spaced_Time-Series)  
13. MetaCycle: an integrated R package to evaluate periodicity in large ..., accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC5079475/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5079475/)  
14. accessed October 1, 2025, [https://cran.r-project.org/web/packages/lomb/lomb.pdf](https://cran.r-project.org/web/packages/lomb/lomb.pdf)  
15. Irregular time series in astronomy and the use of the Lomb-Scargle periodogram \- arXiv, accessed October 1, 2025, [https://arxiv.org/abs/1301.4826](https://arxiv.org/abs/1301.4826)  
16. MetaCycle: Evaluate Periodicity in Large Scale Data \- CRAN, accessed October 1, 2025, [https://cran.r-project.org/web/packages/MetaCycle/MetaCycle.pdf](https://cran.r-project.org/web/packages/MetaCycle/MetaCycle.pdf)  
17. MetaCycle: An integrated R package to evaluate periodicity in large scale data, accessed October 1, 2025, [https://www.researchgate.net/publication/304814567\_MetaCycle\_An\_integrated\_R\_package\_to\_evaluate\_periodicity\_in\_large\_scale\_data](https://www.researchgate.net/publication/304814567_MetaCycle_An_integrated_R_package_to_evaluate_periodicity_in_large_scale_data)  
18. Methods detecting rhythmic gene expression are biologically relevant only for strong signal, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC7100990/](https://pmc.ncbi.nlm.nih.gov/articles/PMC7100990/)  
19. Diffraction Theory Fundamentals | Mathematical Crystallography Class Notes \- Fiveable, accessed October 1, 2025, [https://fiveable.me/mathematical-crystallography/unit-7](https://fiveable.me/mathematical-crystallography/unit-7)  
20. Structure Factors & Fourier Transforms | Mathematical Crystallography Class Notes, accessed October 1, 2025, [https://fiveable.me/mathematical-crystallography/unit-8](https://fiveable.me/mathematical-crystallography/unit-8)  
21. Crystallographic Fourier Analysis \- BioXFEL, accessed October 1, 2025, [https://www.bioxfel.org/science/resources/377/download/Tue\_23\_Sept\_2014\_Crystallographic\_Fourier\_analysis.pdf](https://www.bioxfel.org/science/resources/377/download/Tue_23_Sept_2014_Crystallographic_Fourier_analysis.pdf)  
22. Methodological Considerations for Studying Neural Oscillations \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC8761223/](https://pmc.ncbi.nlm.nih.gov/articles/PMC8761223/)  
23. Calcium and Metabolic Oscillations in Pancreatic Islets: Who's Driving the Bus?\* \- PMC, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC4331037/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4331037/)  
24. Mapping metabolic oscillations during cell cycle progression \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/346086869\_Mapping\_metabolic\_oscillations\_during\_cell\_cycle\_progression](https://www.researchgate.net/publication/346086869_Mapping_metabolic_oscillations_during_cell_cycle_progression)  
25. Engineering Principles of Synthetic Biochemical Oscillators with Negative Cyclic Feedback, accessed October 1, 2025, [http://www.cds.caltech.edu/\~murray/preprints/hm15-cdc\_s.pdf](http://www.cds.caltech.edu/~murray/preprints/hm15-cdc_s.pdf)  
26. Biomolecular Feedback Systems, accessed October 1, 2025, [https://www.cds.caltech.edu/\~murray/books/AM08/pdf/bfs-pupss\_16Jun14.pdf](https://www.cds.caltech.edu/~murray/books/AM08/pdf/bfs-pupss_16Jun14.pdf)  
27. Biomolecular Feedback Systems | Request PDF \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/345683444\_Biomolecular\_Feedback\_Systems](https://www.researchgate.net/publication/345683444_Biomolecular_Feedback_Systems)  
28. Pharmacokinetics & Compartmental Modeling \- Allucent, accessed October 1, 2025, [https://www.allucent.com/resources/blog/compartmental-modeling-pharmacokinetics](https://www.allucent.com/resources/blog/compartmental-modeling-pharmacokinetics)  
29. A semi-compartmental model describing the pharmacokinetic-pharmacodynamic relationship \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC7713860/](https://pmc.ncbi.nlm.nih.gov/articles/PMC7713860/)  
30. Control theory meets synthetic biology \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC4971224/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4971224/)  
31. Enhancing circuit stability under growth feedback with supplementary repressive regulation | Nucleic Acids Research | Oxford Academic, accessed October 1, 2025, [https://academic.oup.com/nar/article/52/3/1512/7504873](https://academic.oup.com/nar/article/52/3/1512/7504873)  
32. Synthetic negative feedback circuits using engineered small RNAs \- PMC \- PubMed Central, accessed October 1, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC6182179/](https://pmc.ncbi.nlm.nih.gov/articles/PMC6182179/)  
33. Platforms for Optogenetic Stimulation and Feedback Control \- Frontiers, accessed October 1, 2025, [https://www.frontiersin.org/journals/bioengineering-and-biotechnology/articles/10.3389/fbioe.2022.918917/full](https://www.frontiersin.org/journals/bioengineering-and-biotechnology/articles/10.3389/fbioe.2022.918917/full)  
34. Real-Time Optogenetics System for Controlling Gene Expression Using a Model-Based Design \- PubMed, accessed October 1, 2025, [https://pubmed.ncbi.nlm.nih.gov/33543619/](https://pubmed.ncbi.nlm.nih.gov/33543619/)  
35. Download Citation \- PLOS Computational Biology, accessed October 1, 2025, [https://journals.plos.org/ploscompbiol/article/citation?id=10.1371/journal.pcbi.1010532](https://journals.plos.org/ploscompbiol/article/citation?id=10.1371/journal.pcbi.1010532)  
36. Graph-based algorithms for Laplace transformed coalescence time distributions | PLOS Computational Biology \- Research journals, accessed October 1, 2025, [https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1010532](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1010532)  
37. (PDF) Fourier transform in Bioinformatics and Biomedicine \- ResearchGate, accessed October 1, 2025, [https://www.researchgate.net/publication/391322539\_Fourier\_transform\_in\_Bioinformatics\_and\_Biomedicine](https://www.researchgate.net/publication/391322539_Fourier_transform_in_Bioinformatics_and_Biomedicine)  
38. Fourier transform in Bioinformatics and Biomedicine \- PubMed, accessed October 1, 2025, [https://pubmed.ncbi.nlm.nih.gov/40636209/](https://pubmed.ncbi.nlm.nih.gov/40636209/)  
39. Fourier transform in Bioinformatics and Biomedicine \- Bioinformation, accessed October 1, 2025, [https://www.bioinformation.net/021/973206300210575.pdf](https://www.bioinformation.net/021/973206300210575.pdf)  
40. Introduction to MetaCycle \- CRAN, accessed October 1, 2025, [https://cran.r-project.org/web/packages/MetaCycle/vignettes/implementation.html](https://cran.r-project.org/web/packages/MetaCycle/vignettes/implementation.html)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAYAAACtWK6eAAAAsUlEQVR4Xu3BAQEAAACCIP+vbkhAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAB8GXHmAAEdo+NeAAAAAElFTkSuQmCC>