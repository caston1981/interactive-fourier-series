

# **Mathematical Foundations of Laplace, Fourier, and Z-Transforms: A Rigorous Analysis of System Lenses**

## **I. Foundational Definitions and Complex Domain Mapping**

The analysis of linear time-invariant (LTI) systems fundamentally relies on a suite of integral and series transformations that convert time-domain operations (convolution, differentiation) into simpler algebraic operations (multiplication, exponentiation). These mathematical tools—the Laplace, Fourier, and Z-Transforms—serve as crucial "lenses" that map signals and systems from their native time domain (![][image1] or ![][image1]) into specialized complex frequency domains, enabling comprehensive analysis of stability, causality, and frequency response.

### **A. The General Integral/Series Transform and Kernel Functions**

The mathematical structure underpinning these techniques is the generalized transform operation. An integral transform is broadly defined as ![][image1], where ![][image1] is the function being transformed, ![][image1] is the resulting function in the new domain, and ![][image1] is the characteristic kernel of the transform.1 The selection of the kernel dictates the properties and applicability of the resulting transform. For the continuous-time domain, the Laplace kernel is the generalized complex exponential,  
![][image1]. For the Fourier Transform, the kernel is the purely oscillatory complex exponential, ![][image1]. In the discrete-time domain, the Z-Transform utilizes the kernel ![][image1] in a summation structure.2

### **B. The Bilateral Laplace Transform (![][image1]): Definition, Domain, and Analyticity**

The Laplace Transform (![][image1]) is the cornerstone for continuous-time (CT) system analysis, particularly for solving linear ordinary differential equations (ODEs) and analyzing dynamical systems.3

#### **Formal Definition:**

The Bilateral Laplace Transform of a function f(t) is defined for suitable functions by the integral:

![][image1]  
Here, s is the complex variable s=σ+jω.3 This definition explicitly incorporates both the exponential decay factor (  
![][image1]) and the oscillatory factor (![][image1]).

#### **Unilateral Form and Causality:**

In control systems and signal processing, causality is often a prerequisite. A causal system's response cannot precede its excitation. The Unilateral Laplace Transform formally enforces this condition by restricting the integration interval:

![][image1]  
This unilateral form is primarily used for causal functions (f(t)=0 for t\<0) and is essential because it naturally incorporates initial conditions (x(0),x′(0), etc.) necessary for solving initial value problems in differential equations.3 The difference between the bilateral and unilateral forms reflects whether the underlying physical system is inherently non-causal or causal.7

#### **Analytic Properties in the ![][image1]\-Plane:**

The Laplace Transform ![][image1] possesses crucial analytic properties within its Region of Convergence (ROC).3 Because  
![][image1] is a function of a complex variable ![][image1], it is often an analytic function in the complex ![][image1]\-plane.3 This analyticity implies that  
![][image1] can be represented by a convergent power series, whose coefficients relate to the moments of the original function.3 The mathematical importance of this analyticity is profound: it allows complex analysis techniques, such as contour integrals and the residue theorem, to be employed for simplifying calculations and for the rigorous inversion of the transform.3 The transformation converts analytic problems, specifically differential equations, into algebraic problems in the  
![][image1]\-domain.3

### **C. The Fourier Transform (![][image1]): Representation, Limits, and Unitary Properties**

The Fourier Transform (![][image1]) provides the spectral representation of a signal, describing the extent to which various frequencies (![][image1]) are present.9

#### **Definition and Domain:**

The Continuous-Time Fourier Transform (CTFT) is defined as:

![][image1]  
The Fourier transform is formally a function of the purely imaginary variable jω.1

#### **The ![][image1] Transform as a Projection of ![][image1]:**

The Fourier Transform is a specialized case, or projection, of the Bilateral Laplace Transform. Mathematically, the relationship is established by evaluating the Laplace Transform on the imaginary axis of the ![][image1]\-plane: ![][image1].5 This identity is only rigorously valid if the imaginary axis,  
![][image1], is included within the Region of Convergence (ROC) of the Laplace Transform ![][image1].5  
The ROC must include the ![][image1] axis for the Fourier transform to be defined, a condition that holds significant physical meaning: it is the necessary and sufficient condition for the continuous-time system to exhibit Bounded Input Bounded Output (BIBO) stability.7 If the system is unstable (not BIBO stable), the  
![][image1] axis is excluded from the ROC, and only the Laplace Transform ![][image1] is rigorously defined, not ![][image1].7

#### **Unitary Structure and Plancherel's Theorem:**

The Fourier Transform exhibits a crucial unitary property. Plancherel's Theorem formalizes this property, stating that the energy (the squared modulus integral) of a function in the time domain is proportional to the energy in the frequency domain.10  
![][image1]  
This theorem confirms that the F transform is a unitary operator on L2(R), preserving the signal's energy.10 This conservation property is central to many applications in harmonic analysis.

### **D. The Z-Transform (![][image1]): Formal Definition as a Laurent Series and the ![][image1]\-Plane**

The Z-Transform (![][image1]) serves as the discrete-time analogue of the Laplace Transform, applying to sequences ![][image1] defined over integers ![][image1].12

#### **Formal Definition:**

The Bilateral Z-Transform of a discrete sequence x\[n\] is defined by the infinite series:

![][image1]  
The variable z is a complex number, z=rejω.2 This transform is essential for solving linear difference equations, the discrete counterpart to differential equations.5

#### **Connection to Laurent Series:**

Crucially, the power series defining the Z-Transform, ![][image1], is formally recognized as a Laurent series centered at ![][image1].13 This classification has profound implications for the analytic properties of  
![][image1]. Since the Z-Transform is a Laurent series, it represents an analytic function at every point inside its Region of Convergence (ROC).13 Consequently,  
![][image1] and all its derivatives must be continuous functions of ![][image1] within the ROC, enabling the powerful use of complex analysis methods for its inversion.13

#### **The Discrete-Time Fourier Transform (DTFT) as an Evaluation of ![][image1]:**

The Discrete-Time Fourier Transform (DTFT) is the discrete equivalent of the continuous Fourier transform:

![][image1]  
Similar to the L/F relationship, the DTFT is obtained by evaluating the Z-Transform on the boundary defined by ∣z∣=1, i.e., z=ejω.2  
![][image1]  
This evaluation is only permissible if the unit circle lies within the ROC of X(z).2 This boundary evaluation provides the system's periodic frequency response, typically plotted between  
![][image1] and ![][image1] radians, reflecting the ![][image1] periodicity of the DTFT.16

### **E. The Analytic Hierarchy of Transform Domains**

A detailed examination of these definitions reveals an inherent analytic hierarchy. The Laplace (![][image1]) and Z-Transforms (![][image1]) function as powerful analytic extensions of the Fourier (![][image1]) and DTFT, respectively, allowing transient and stability analysis to move beyond steady-state frequency characterization.  
The Fourier transform, being a special case where ![][image1], requires the system to be highly constrained, specifically demanding that the ![][image1] axis be included in the convergence region.7 If a continuous system is unstable,  
![][image1] ceases to exist in the formal sense.7 In contrast,  
![][image1] allows for ![][image1], permitting the integral to converge even if the time-domain function ![][image1] exhibits exponential growth that prevents absolute integrability.4 This ability to handle non-  
![][image1] functions by shifting the axis of integration is what grants ![][image1] its analytical superiority in control theory.  
This relationship confirms that ![][image1] and ![][image1] sit at a higher mathematical complexity level rooted in complex analysis. Because ![][image1] and ![][image1] are analytic in their respective ROCs 3, the behavior of the transform function across the entire complex plane is uniquely determined by its values on the boundary (the  
![][image1] or DTFT evaluation), a process related to analytic continuation. Consequently, when a system is unstable and the frequency transform is undefined, the ![][image1] and ![][image1] transforms remain mathematically defined in a non-inclusive ROC, allowing system properties, such as pole locations, to be analyzed algebraically.3 This capability to transform an analytic problem into a tractable algebraic problem underscores their primary value in the analysis of dynamic systems.  
---

## **II. Convergence Criteria and Analytic Properties**

The existence and interpretation of the Laplace, Fourier, and Z-Transforms are predicated entirely upon the convergence of their defining integral or series. The Region of Convergence (ROC) mathematically dictates the set of complex variables for which the transform is defined and directly encodes fundamental properties of the system, such as causality and stability.

### **A. Defining the Region of Convergence (ROC): Mathematical Existence**

The ROC specifies the range of the complex variable (![][image1] or ![][image1]) for which the defining summation or integral yields a finite value.17 The transform function  
![][image1] or ![][image1] is only defined within this region.15

#### **Laplace Transform ROC:**

For ![][image1], the ROC is determined by the real part of ![][image1], ![][image1]. Since ![][image1], the magnitude term ![][image1] simplifies to ![][image1]. The integral ![][image1] converges when ![][image1] decays sufficiently quickly to offset any exponential growth in ![][image1]. The ROC is typically a vertical strip or a half-plane in the ![][image1]\-plane (![][image1]).3  
Convergence for the unilateral Laplace transform demands that ![][image1] satisfy the Dirichlet conditions: ![][image1] must be piecewise continuous, and critically, ![][image1] must be of exponential order.4 A function  
![][image1] is of exponential order if there exist positive constants ![][image1] and ![][image1] such that ![][image1] for all ![][image1].4 If this condition holds, the integral converges for all  
![][image1].

#### **Z-Transform ROC:**

For ![][image1], the convergence depends on the magnitude of ![][image1], denoted by ![][image1]. The series ![][image1] converges for specific values of ![][image1]. For general two-sided sequences, the ROC is defined as an annulus in the ![][image1]\-plane (![][image1]).17 The radii  
![][image1] and ![][image1] are determined by the magnitudes of the innermost and outermost poles of the transfer function.17

### **B. Absolute vs. Conditional Convergence**

The distinction between types of convergence is essential for understanding the mathematical robustness of transforms, particularly the Fourier and DTFT.18

#### **Definitions:**

A series or integral converges *absolutely* if the summation or integration of the absolute value of the function converges: ![][image1] or ![][image1].19 If the original series/integral converges, but the absolute value does not, the convergence is  
*conditional*.18

#### **Mathematical Significance:**

Absolute convergence represents a stronger form of convergence.19 For discrete series, absolute convergence guarantees that any rearrangement of the terms will result in the same sum. Conditional convergence lacks this property, meaning rearrangement can potentially change the resulting value.19 This stability in mathematical manipulation is why absolute convergence is tied directly to the physical stability of systems, as discussed below.

### **C. Role of Poles and Zeros in Determining ROC Geometry**

The singularities (poles) of the rational transform function fundamentally define the boundaries of the ROC. By definition, the ROC can never contain a pole.15

#### **Causality and ROC Geometry:**

The geometry of the ROC is inextricably linked to the causality of the system's impulse response.

1. **Causal (Right-Sided) Systems:** For a causal sequence ![][image1] or function ![][image1] (defined for ![][image1] or ![][image1]), the ROC is the exterior of a circle in the ![][image1]\-plane, specifically the region outside the outermost pole.17 For the  
   ![][image1] transform, the ROC is a right half-plane.  
2. **Anti-Causal (Left-Sided) Systems:** For an anti-causal system (defined for ![][image1] or ![][image1]), the ROC is the interior of a circle in the ![][image1]\-plane, specifically the region inside the innermost pole.17

#### **Stability and ROC Inclusion:**

The rigorous condition for Bounded-Input Bounded-Output (BIBO) stability is defined by the inclusion of the frequency axis within the ROC.21

* For continuous-time systems (Laplace), BIBO stability is achieved if and only if the ROC includes the entire ![][image1] axis (![][image1]).7  
* For discrete-time systems (Z-Transform), BIBO stability is achieved if and only if the ROC includes the unit circle (![][image1]).20

### **D. Absolute Convergence as the Foundation of Strong BIBO Stability**

The mathematical requirement for absolute integrability or summability of the impulse response is the foundation for robust BIBO stability in LTI systems. This fundamental requirement is precisely equivalent to the ROC including the stability boundary.  
BIBO stability requires that a bounded input signal ![][image1] must always produce a bounded output signal ![][image1].22 Based on the convolution theorem, this physical requirement imposes a mathematical constraint on the impulse response  
![][image1]. For CT systems, stability demands ![][image1] (absolute integrability). For DT systems, stability requires ![][image1] (absolute summability).  
The convergence condition for the Fourier transform is ![][image1]. Since the magnitude ![][image1] is identically 1, the integral converges absolutely if and only if ![][image1] is absolutely integrable. Therefore, absolute integrability in the time domain is the rigorous mathematical condition for the resulting frequency transform (Fourier or DTFT) to exist, which ensures the stability guarantee.7 If the Fourier transform only converges conditionally, the system may be marginally stable or may violate BIBO stability for specific inputs. Absolute convergence is the rigorous mathematical guarantee of system stability and robustness.  
---

## **III. Inter-Domain Transformations and Discretization Mapping**

The three transforms are related through precise mathematical transformations and projections. Of particular engineering interest is the transformation from continuous-time (CT, ![][image1]\-plane) to discrete-time (DT, ![][image1]\-plane), which requires complex mapping functions to translate stability and frequency characteristics accurately.

### **A. The ![][image1] and DTFT Projections: Conditions for Evaluation**

The Fourier and DTFT provide the steady-state frequency domain view, derived by evaluating their generalized counterparts on the complex stability boundaries.

#### **Laplace ![][image1] Fourier Projection:**

The continuous frequency response is obtained by setting ![][image1] in ![][image1]. As previously established, this is only mathematically permissible if the ![][image1] axis is contained within the ROC of ![][image1].5 This inclusion is the definitive necessary and sufficient condition for continuous LTI system BIBO stability.7

#### **Z-Transform ![][image1] DTFT Projection:**

Similarly, the discrete frequency response ![][image1] is obtained by evaluating ![][image1] on the unit circle, ![][image1]. This step is only valid if the unit circle ![][image1] lies within the ROC.2 This boundary evaluation yields the system's gain and phase response as a function of discrete frequency  
![][image1].

### **B. Discretization Techniques: Mapping the ![][image1]\-Plane to the ![][image1]\-Plane**

Discretization is the process of generating a DT system transfer function ![][image1] that closely approximates a CT system transfer function ![][image1], typically defined by the mapping ![][image1].

#### **The Euler Approximations (Forward and Backward):**

Discretization of differential equations often relies on approximating the derivative operator ![][image1] using finite differences based on the Taylor series expansion of ![][image1], where ![][image1] is the sampling interval.

1. Forward Euler (Forward Difference): This method approximates the derivative at time t using the current value and the next value: dtdy​≈Ty\[n+1\]−y\[n\]​. In the transform domain, this leads to the mapping:  
   ![][image1]  
2. Backward Euler (Backward Difference): This method approximates the derivative using the current value and the past value: dtdy​≈Ty\[n\]−y\[n−1\]​. In the transform domain, this leads to the mapping:  
   ![][image1]

These Euler methods are first-order numerical procedures.23 They introduce significant local truncation error (proportional to  
![][image1]) and global discretization error (proportional to ![][image1]).24 Furthermore, their stability mapping is mathematically weak. For instance, the forward Euler method may map parts of the stable Left Half-Plane (LHP) of the  
![][image1]\-domain to regions outside the unit circle in the ![][image1]\-domain, potentially converting a stable CT system into an unstable DT realization.26

#### **The Bilinear Transform (Tustin's Method): Rigorous Derivation and Warping**

The Bilinear Transform (also known as Tustin's method) is the preferred technique in digital signal processing and discrete-time control due to its superior stability preservation properties.27

1. Mathematical Derivation: The Bilinear Transform is derived by approximating the continuous-time integration operator 1/s using the trapezoidal rule for numerical integration, which is superior to the first-order rectangular approximations used by the Euler methods. The resulting algebraic mapping is defined as:  
   ![][image1]  
   28  
2. **Stability Preservation Proof:** The central feature of the Bilinear Transform is its exact, one-to-one mapping of the stability boundaries. It performs a conformal transformation that maps the entire open Left Half-Plane (![][image1]) in the ![][image1]\-domain exactly onto the interior of the Unit Circle (![][image1]) in the ![][image1]\-domain.27 This mathematically guarantees that any stable CT filter designed in the  
   ![][image1]\-domain is converted into a stable DT filter in the ![][image1]\-domain.29 Similarly, minimum-phase properties (zeros in the LHP) are preserved by mapping zeros to the interior of the unit circle.27  
3. **Frequency Warping:** The robust stability preservation comes at a cost: the mapping of the frequency axes is nonlinear, leading to frequency warping.28 The imaginary axis of the  
   ![][image1]\-plane (![][image1]) is mapped precisely to the unit circle of the ![][image1]\-plane (![][image1]).27 The relationship between the continuous frequency  
   ωa​ (analog) and the discrete frequency ωd​ (digital) is given by:  
   ![][image1]  
   27

   This means the infinite continuous frequency range (−∞\<ωa​\<∞) is compressed onto the finite discrete frequency range (−π/T≤ωd​≤π/T).28 This compression is necessary to preserve the stability topology but distorts the linear frequency response unless pre-warping techniques are employed.

### **C. Topological Necessity of the Bilinear Transform**

The superiority of the Bilinear Transform in digital filter design stems from its robust topological mapping, which is essential for stable discretization, even at the expense of frequency accuracy.  
The objective of discretization is the reliable translation of the system dynamics ![][image1] to ![][image1] while preserving system stability.29 The continuous-time stability region, the Left Half-Plane (LHP), is an infinitely large region. The discrete-time stability region, the interior of the unit circle, is finite. Any successful mapping must map this infinite space into a finite space without distorting the stability boundary crossings. Simpler numerical approximations, such as the Euler methods, fail because they rely on localized, first-order approximations, leading to inaccurate stability mappings for larger sampling intervals.26  
The Bilinear Transform achieves this by executing a conformal mapping that correctly compresses the infinite ![][image1] axis onto the finite unit circle boundary.27 This robust preservation of the stability boundary relationship guarantees the integrity of the system in the discrete domain. Therefore, the resultant frequency warping is not a mathematical defect but is an unavoidable consequence of mapping an infinite stability region (LHP) to a finite stability region (unit disk) while maintaining the integrity of the pole locations relative to the critical stability boundary.  
Table 3: Inter-Domain Mapping Properties (Continuous to Discrete)

| Property | Laplace Transform (![][image1]) / ![][image1]\-Domain | Z-Transform (![][image1]) / ![][image1]\-Domain | Mapping Method | Mathematical Consequence |
| :---- | :---- | :---- | :---- | :---- |
| **Stability Region** | Left Half-Plane ![][image1] | Unit Circle Interior $ | z | \< 1$ |
| **Frequency Axis Mapping** | **![][image1]** axis (![][image1]) | Unit Circle $ | z | \=1$ (![][image1]) |
| **Inverse Formula Basis** | Bromwich Integral | Contour Integral ![][image1] | Complex Analysis | Evaluation via Cauchy's Residue Theorem 30 |

---

## **IV. Complex Analysis for Transform Inversion and Properties**

While the transforms simplify operations in the frequency domains, the inverse transformations—reverting back to the time domain—often require sophisticated mathematical tools rooted in complex variable theory, particularly Cauchy's Residue Theorem.

### **A. The Fourier Inversion Theorem and Uniqueness**

A core strength of the transform methods is their invertibility, ensuring that the process of transforming and inverting does not lose information.32

#### **Fourier Inversion Theorem:**

For the Fourier Transform, the inverse operation is rigorously defined by the inversion integral:

![][image1]33

The existence of this inverse formula is closely related to the Fourier Inversion Theorem, which forms the basis for deriving the inverse Laplace transform.33

#### **Uniqueness:**

For any given transform ![][image1] or ![][image1] within its ROC, the corresponding time-domain function ![][image1] or sequence ![][image1] is unique.33 This bijective mapping is critical for analysis, guaranteeing that the solution found in the algebraic domain corresponds to one and only one physical behavior in the time domain.

### **B. Inverse Laplace Transform: The Bromwich Integral and Residue Calculus**

The inverse Laplace transform cannot generally be computed using simple integration along the real axis. It requires integration in the complex ![][image1]\-plane.

#### **The Bromwich Integral (Mellin's Inverse Formula):**

The formal mathematical definition of the inverse Laplace transform is given by the line integral, often termed the Bromwich integral or the Fourier–Mellin integral:

![][image1]30

The integration is performed along a vertical contour C in the s-plane, denoted by Re(s)=γ. The value γ must be chosen such that the vertical line lies entirely within the ROC of F(s).30

#### **Application of Cauchy's Residue Theorem:**

Direct evaluation of the Bromwich integral is typically challenging. In practice, for rational functions ![][image1], the integral is evaluated using Cauchy's Residue Theorem. The contour is closed by adding a large semi-circular arc (the Bromwich contour) to the left of the vertical line, ensuring that all poles of ![][image1] are enclosed.35 The inverse transform  
f(t) is then calculated as the sum of the residues of the function F(s)est at all poles pk​ enclosed by the contour:

![][image1]35

This technique effectively converts the difficult complex line integration into a much simpler algebraic calculation involving residue computation.35

### **C. Inverse Z-Transform: Contour Integration**

The inversion of the Z-Transform similarly requires complex contour integration.31

#### **The Formal Inverse:**

The Inverse Z-Transform for a sequence x\[n\] is defined by the contour integral:

![][image1]31

The contour C must be a closed, counter-clockwise path entirely contained within the ROC of X(z) and must encircle the origin of the z-plane.31

#### **Residue Theorem Application:**

When X(z) is a rational function, the inverse sequence x\[n\] can be found by applying Cauchy's Residue Theorem to the integrand X(z)zn−1. The result is the sum of the residues of this function at all poles pk​ that are located inside the contour C:

![][image1]31

This powerful algebraic technique avoids direct integration and is valid for both positive and negative indices n.31

### **D. Fundamental Transform Theorems**

The primary utility of these transforms is derived from their operational properties that simplify complex time-domain manipulations.

#### **Convolution Theorem:**

The Convolution Theorem is perhaps the most critical mathematical property for LTI system analysis. It states that convolution in the time domain corresponds to simple point-wise multiplication in the transform domain.38  
![][image1]![][image1]  
This transformation converts the computation of system output (y=x∗h) from a complex integration/summation operation into straightforward multiplication, making the analysis of coupled systems highly tractable.38

#### **Differentiation and Integration Properties:**

In the Laplace domain, differentiation in the time domain ![][image1] is mapped to multiplication by ![][image1] (incorporating initial conditions).3 This property directly facilitates the conversion of linear differential equations into algebraic polynomial equations.3 Similarly, integration in the time domain is mapped to division by  
![][image1].40  
![][image1]

#### **Time Shifting Property:**

A shift in the time variable corresponds to multiplication by an exponential term in the transform domain.6  
![][image1]![][image1]  
This property is vital for analyzing delays and delays in physical and discrete systems.6

### **E. The Transform as an Operator Eigenfunction**

The core reason the Convolution Theorem simplifies system analysis lies in the mathematical nature of the kernel functions. The complex exponentials (![][image1] and ![][image1]) utilized in the transform definitions are the *eigenfunctions* of all LTI systems.  
For an LTI system defined by impulse response h(t), if the input is the complex exponential x(t)=est, the output is y(t)=h(t)∗est. This convolution simplifies to:

![][image1]  
The output y(t) is simply the input est scaled by a complex constant H(s). The function H(s) is the eigenvalue corresponding to the eigenfunction est.38 The Laplace transform  
![][image1] (and ![][image1]) is, therefore, the characteristic response, or eigenvalue, of the system when excited by its own basis function. This decomposition converts the complexity of time-domain dynamics into a straightforward algebraic relationship in the transform domain, forming the basis for spectral theory in functional analysis.43  
---

## **V. Transforms as Unified Lenses for System Analysis**

The application of ![][image1] and ![][image1] transforms provides a unified framework for assessing fundamental system characteristics, notably causality and BIBO stability, through the geometric location of poles in the complex plane.

### **A. Causality and the ROC**

Causality is a physical constraint that translates directly into a mathematical condition on the impulse response ![][image1], requiring ![][image1] for ![][image1] (CT) or ![][image1] for ![][image1] (DT).  
In the transform domain, causality is determined by the shape of the ROC relative to the system's poles. For systems defined by rational transfer functions, a system is causal if and only if its ROC is the exterior region, extending outward from the pole with the largest magnitude.17 For the Laplace domain, this translates to a right half-plane ROC. When using the unilateral Laplace transform, the integration limits from  
![][image1] to ![][image1] automatically enforce the causality condition ![][image1].3

### **B. Bounded-Input Bounded-Output (BIBO) Stability**

BIBO stability is the essential requirement that prevents a system from producing unbounded output responses to finite excitations.22 The stability of an LTI system is geometrically defined by the location of the poles of its transfer function  
![][image1].

#### **Stability and the ROC (Unified Criterion):**

The unified mathematical criterion for BIBO stability requires that the ROC of the system transfer function must include the frequency boundary.21

1. **Continuous-Time LTI Systems:** Stability requires the ROC of ![][image1] to include the ![][image1] axis (![][image1]). This condition is met if and only if all poles of ![][image1] lie strictly in the Open Left Half-Plane (LHP), meaning ![][image1].44  
2. **Discrete-Time LTI Systems:** Stability requires the ROC of ![][image1] to include the unit circle (![][image1]). This condition is met if and only if all poles of ![][image1] lie strictly inside the unit circle, meaning ![][image1].21

### **C. Continuous-Time Stability: The Routh–Hurwitz Criterion**

To analyze the stability of a CT system described by a characteristic polynomial ![][image1], the Routh–Hurwitz criterion provides an algebraic method to determine if all roots (poles) lie in the LHP without explicitly solving for the roots.45

#### **The Criterion:**

The Routh–Hurwitz criterion relies on constructing a Routh array from the coefficients of the characteristic polynomial ![][image1]. The stability status is determined by counting the sign changes in the first column of this array. The number of sign changes directly corresponds to the number of roots with positive real parts (poles in the RHP, ![][image1]).45

#### **Mathematical Derivation:**

The mathematical basis of the Routh test originates from the Routh–Hurwitz theorem, which relates the pole counts to the generalized Sturm chain and Cauchy indices.45 A polynomial  
![][image1] is considered Hurwitz stable (all roots in the LHP) if and only if the number of roots in the LHP (![][image1]) minus the number of roots in the RHP (![][image1]) equals the degree of the polynomial (![][image1]), i.e., ![][image1].45 Since  
![][image1] (by the fundamental theorem of algebra, assuming no roots on the ![][image1] axis), stability requires ![][image1], or ![][image1].45 The Routh array provides a simple computational mechanism to verify this condition.

### **D. Discrete-Time Stability: The Jury Criterion**

The Jury stability criterion is the established discrete-time analogue of the Routh–Hurwitz criterion, designed for analyzing DT systems in the ![][image1]\-domain.46

#### **The Criterion:**

For a DT system, stability requires all poles of the characteristic polynomial ![][image1] to lie strictly inside the unit circle.22 The Jury test involves constructing a Jury stability table based on the coefficients of  
![][image1]. Specific criteria applied to the coefficients and the resulting rows of the table determine if all roots satisfy the ![][image1] condition.47 The process iteratively reduces the degree of the polynomial, ensuring all coefficients meet necessary constraints for stability.46  
Table 2: Domain Stability Criteria and Associated Theorems

| Domain | System Type | Stability Criterion (BIBO) | Causality Criterion (ROC) | Characteristic Polynomial Theorem |
| :---- | :---- | :---- | :---- | :---- |
| **![][image1]**\-Plane | Continuous-Time LTI | All Poles in Open Left Half-Plane (![][image1]) 44 | ROC is a right half-plane 20 | Routh–Hurwitz Criterion 45 |
| ![][image1]\-Plane | Discrete-Time LTI | All Poles Inside the Unit Circle ($ | z | \<1$) 21 |
| Boundary Condition | LTI (General) | ROC must include the stability boundary (![][image1] axis or Unit Circle) 21 | Defined by pole location relative to ROC boundary 20 | N/A |

### **E. Theoretic Unification via Time Scales Calculus**

A rigorous mathematical framework unifies the Laplace and Z-Transforms under a single generalized operator: Time Scales Calculus (or analysis on measure chains).48  
This calculus operates on arbitrary "time scales" or "measure chains" (![][image1]), which can be the continuous real numbers (![][image1]) or the discrete integers (![][image1]).48 Within this framework, a generalized Laplace transform is defined. If the time scale is chosen as  
![][image1], the generalized definition reduces precisely to the standard Laplace Transform. If the time scale is chosen as ![][image1], the generalized definition reduces to the standard Z-Transform.48 This demonstrates that the two transforms are not separate inventions but specific manifestations of the same underlying mathematical structure tailored for continuous or discrete domains.  
In the higher realm of functional analysis, this structure is linked to Spectral Theory.43 The transforms provide the spectrum (eigenvalues) of the differential operator (  
![][image1]) for continuous systems or the difference operator for discrete systems.43 By translating the problem into the transform domain, one is effectively analyzing the system through its spectral decomposition, confirming why LTI system analysis is fundamentally algebraic in nature.

### **F. The Pole-Zero Map as the "Spectrum" of the LTI Operator**

The geometric location of poles and zeros in the complex plane (![][image1] or ![][image1]) provides a complete, concise map of all fundamental system characteristics, acting as the system's inherent "spectrum".43  
Since the transforms convert the infinite-dimensional complexity of the time-domain impulse response into a rational function (a finite-dimensional algebraic problem), the pole and zero locations define the system's behavior.50 Poles, being the roots of the denominator, dictate the natural exponential modes of the system response (  
![][image1] or ![][image1]).50 Their placement relative to the stability boundary (  
![][image1] or ![][image1]) governs stability through the Routh–Hurwitz and Jury criteria.45  
Furthermore, the pole locations relative to the ROC define causality.20 The complex plane geometry also allows for the geometric evaluation of the frequency response: the magnitude and phase response at a given frequency point on the boundary (  
![][image1] or the unit circle) can be visually determined by measuring the lengths and angles of vectors drawn from the poles and zeros to that frequency point.16 Thus, the pole-zero map is a topologically robust representation encompassing stability, causality, and frequency dynamics in one powerful algebraic structure.  
---

## **VI. Detailed Topics in Signal Fidelity and Aliasing**

The mathematical relationship between the continuous Fourier domain and the discrete Fourier domain (DTFT) provides the essential link for understanding the process of sampling and the errors introduced therein.

### **A. The Nyquist–Shannon Sampling Theorem**

The Nyquist–Shannon Sampling Theorem establishes the mathematical conditions required for the perfect reconstruction of a continuous-time signal from its discrete samples.51

#### **Mathematical Statement:**

If a continuous-time signal ![][image1] is strictly band-limited, containing no frequency components higher than ![][image1] hertz, then ![][image1] can be completely determined from its samples ![][image1] if the sampling rate ![][image1] is strictly greater than ![][image1].51 The frequency  
![][image1] is the Nyquist frequency, and ![][image1] is the Nyquist rate.

#### **Proof Context:**

The formal proof relies on the fact that the Fourier Transform ![][image1] of a band-limited signal is zero outside the interval $$. When sampled, the resulting spectrum ![][image1] is a periodic repetition of ![][image1]. If the sampling rate is adequate, these repetitions do not overlap, allowing the original spectrum to be isolated and recovered via a low-pass filter (which corresponds to a sinc interpolation in the time domain).51

### **B. The Rigor of Aliasing and the Poisson Summation Formula**

When the sampling rate ![][image1] is less than the Nyquist rate ![][image1] (undersampling), a phenomenon known as aliasing occurs, where high-frequency components in the original signal are mistakenly interpreted as lower-frequency components in the reconstructed signal.52

#### **Poisson Summation Formula (PSF):**

The Poisson Summation Formula provides the rigorous mathematical link between the continuous spectrum ![][image1] and the discrete, periodic spectrum ![][image1]. The PSF relates the summation of a sampled time function to the summation of its periodic spectrum.54  
![][image1]  
The left side is the DTFT scaled by T. The right side shows that the spectrum of the sampled signal is an infinite summation of shifted (periodic) copies of the original continuous spectrum F(ω), scaled by 1/T.54

#### **Spectral Overlap:**

The condition for aliasing is mathematically visible in the PSF. If the shift term ![][image1] (which is ![][image1]) is less than twice the bandwidth ![][image1], the shifted copies of ![][image1] overlap.52 This spectral overlap means that energy from higher frequency copies (or "aliases") spills into the baseband (  
![][image1]), causing reconstruction errors.52 The PSF rigorously defines the underlying mathematical mechanism of this frequency confusion.

### **C. Rigorous Treatment of Generalized Functions (Dirac Delta)**

The foundation of LTI system analysis, the impulse response ![][image1], requires the use of generalized functions, specifically the Dirac delta function ![][image1].  
The Dirac delta function is defined not by its value at ![][image1] (which is infinite 56) but by its properties as a distribution (or generalized function):  
![][image1]56

The rigorous treatment of the transforms of these functions requires extending the analysis into the theory of distributions, especially when dealing with the boundary of the complex plane.43  
The Laplace transform, however, handles the Dirac delta smoothly because the transform itself is defined through integration, which inherently suits generalized functions:

![][image1]3

The ability of the Laplace transform to algebraically represent the impulsive stimulus (transferring δ(t) to 1\) is crucial for defining the transfer function H(s)=L{h(t)}, which forms the basis for all LTI system analysis.

## **Conclusions**

The Laplace, Fourier, and Z-Transforms constitute a unified mathematical toolkit essential for the analysis and design of LTI systems. The investigation reveals a fundamental analytic hierarchy: ![][image1] and ![][image1] serve as powerful analytic extensions, permitting stability analysis in the full complex plane where the restricted ![][image1] and DTFT might fail to converge due to system instability.  
The mathematical rigor hinges upon complex analysis. System existence is governed by the Region of Convergence (ROC), where the geometry of the ROC relative to the pole locations defines causality, and the inclusion of the frequency boundary (![][image1] axis or unit circle) defines BIBO stability. The transformation between continuous and discrete domains is governed by topological necessity; specifically, the Bilinear Transform is mandated to ensure that stable systems remain stable, even though this requires mathematically necessary frequency warping.  
Ultimately, these transforms empower control system and signal processing engineers by reducing complex operations in the time domain—convolution and differentiation—to simple algebraic operations in the complex domains. The pole-zero map acts as the system's "spectrum," providing a complete, geometric visualization of all fundamental system characteristics—stability, causality, and frequency response—a powerful testament to the mathematical elegance of frequency domain analysis.

#### **Works cited**

1. 5 Fourier and Laplace Transforms \- UNCW, accessed September 30, 2025, [https://people.uncw.edu/hermanr/mat367/fcabook/Transforms.pdf](https://people.uncw.edu/hermanr/mat367/fcabook/Transforms.pdf)  
2. The Z-Transform \- Moodle@Units, accessed September 30, 2025, [https://moodle2.units.it/pluginfile.php/600542/mod\_folder/content/0/Slides%2005%20The%20Z%20Transform.pdf?forcedownload=1](https://moodle2.units.it/pluginfile.php/600542/mod_folder/content/0/Slides%2005%20The%20Z%20Transform.pdf?forcedownload=1)  
3. Laplace transform \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Laplace\_transform](https://en.wikipedia.org/wiki/Laplace_transform)  
4. LAPLACE TRANSFORMS AND ITS APPLICATIONS, accessed September 30, 2025, [https://sces.phys.utk.edu/\~moreo/mm08/sarina.pdf](https://sces.phys.utk.edu/~moreo/mm08/sarina.pdf)  
5. Relation and difference between Fourier, Laplace and Z transforms \- Electrical Engineering Stack Exchange, accessed September 30, 2025, [https://electronics.stackexchange.com/questions/86489/relation-and-difference-between-fourier-laplace-and-z-transforms](https://electronics.stackexchange.com/questions/86489/relation-and-difference-between-fourier-laplace-and-z-transforms)  
6. Time Shifting Property of Laplace Transform \- Tutorials Point, accessed September 30, 2025, [https://www.tutorialspoint.com/time-shifting-property-of-laplace-transform](https://www.tutorialspoint.com/time-shifting-property-of-laplace-transform)  
7. Unilateral Laplace Transform vs Bilateral Fourier Transform \- Mathematics Stack Exchange, accessed September 30, 2025, [https://math.stackexchange.com/questions/1719754/unilateral-laplace-transform-vs-bilateral-fourier-transform](https://math.stackexchange.com/questions/1719754/unilateral-laplace-transform-vs-bilateral-fourier-transform)  
8. 13: Laplace Transform \- Mathematics LibreTexts, accessed September 30, 2025, [https://math.libretexts.org/Bookshelves/Analysis/Complex\_Variables\_with\_Applications\_(Orloff)/13%3A\_Laplace\_Transform](https://math.libretexts.org/Bookshelves/Analysis/Complex_Variables_with_Applications_\(Orloff\)/13%3A_Laplace_Transform)  
9. Fourier transform \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Fourier\_transform](https://en.wikipedia.org/wiki/Fourier_transform)  
10. Plancherel theorem \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Plancherel\_theorem](https://en.wikipedia.org/wiki/Plancherel_theorem)  
11. Plancherel's Theorem \-- from Wolfram MathWorld, accessed September 30, 2025, [https://mathworld.wolfram.com/PlancherelsTheorem.html](https://mathworld.wolfram.com/PlancherelsTheorem.html)  
12. The z Transform \- UTK-EECS, accessed September 30, 2025, [https://web.eecs.utk.edu/\~mjr/ECE503/PresentationSlides/Chapter11Slides.pdf](https://web.eecs.utk.edu/~mjr/ECE503/PresentationSlides/Chapter11Slides.pdf)  
13. The z-Transform, accessed September 30, 2025, [http://ggn.dronacharya.info/EEEDept/Downloads/QuestionBank/VIISem/DSP/SectionB/LECTURE17-18.pdf](http://ggn.dronacharya.info/EEEDept/Downloads/QuestionBank/VIISem/DSP/SectionB/LECTURE17-18.pdf)  
14. Fourier transform derivation from Laurent series \- MathOverflow, accessed September 30, 2025, [https://mathoverflow.net/questions/349998/fourier-transform-derivation-from-laurent-series](https://mathoverflow.net/questions/349998/fourier-transform-derivation-from-laurent-series)  
15. Z-transforms : Part I 1 Relation to Discrete-Time Fourier Transform \- MIT, accessed September 30, 2025, [https://courses.media.mit.edu/2007fall/mas160/zI.pdf](https://courses.media.mit.edu/2007fall/mas160/zI.pdf)  
16. Discrete-Time Fourier Transform from Z-Transform \- YouTube, accessed September 30, 2025, [https://www.youtube.com/watch?v=rhcDfn803ec](https://www.youtube.com/watch?v=rhcDfn803ec)  
17. Region of Convergence, Properties, Stability and Causality of Z-transforms \- Technobyte, accessed September 30, 2025, [https://technobyte.org/roc-properties-z-transform-stability-causality/](https://technobyte.org/roc-properties-z-transform-stability-causality/)  
18. Conditional & absolute convergence (video) \- Khan Academy, accessed September 30, 2025, [https://www.khanacademy.org/math/ap-calculus-bc/bc-series-new/bc-10-9/v/conditional-and-absolute-convergence](https://www.khanacademy.org/math/ap-calculus-bc/bc-series-new/bc-10-9/v/conditional-and-absolute-convergence)  
19. Calculus II \- Absolute Convergence \- Pauls Online Math Notes, accessed September 30, 2025, [https://tutorial.math.lamar.edu/classes/calcii/absoluteconvergence.aspx](https://tutorial.math.lamar.edu/classes/calcii/absoluteconvergence.aspx)  
20. Pole–zero plot \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Pole%E2%80%93zero\_plot](https://en.wikipedia.org/wiki/Pole%E2%80%93zero_plot)  
21. BIBO stability \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/BIBO\_stability](https://en.wikipedia.org/wiki/BIBO_stability)  
22. BIBO Stability \- (Intro to Electrical Engineering) \- Vocab, Definition, Explanations | Fiveable, accessed September 30, 2025, [https://fiveable.me/key-terms/introduction-electrical-systems-engineering-devices/bibo-stability](https://fiveable.me/key-terms/introduction-electrical-systems-engineering-devices/bibo-stability)  
23. Euler method \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Euler\_method](https://en.wikipedia.org/wiki/Euler_method)  
24. Error Bounds for Euler's Method \- Ximera \- The Ohio State University, accessed September 30, 2025, [https://ximera.osu.edu/laode/textbook/numericalSolutionsOfODEs/errorBoundsForEulersMethod](https://ximera.osu.edu/laode/textbook/numericalSolutionsOfODEs/errorBoundsForEulersMethod)  
25. Error Analysis of the Euler Method \- UBC Math, accessed September 30, 2025, [https://www.math.ubc.ca/\~israel/m215/euler2/euler2.html](https://www.math.ubc.ca/~israel/m215/euler2/euler2.html)  
26. Justification of bilinear transform \- Signal Processing Stack Exchange, accessed September 30, 2025, [https://dsp.stackexchange.com/questions/62752/justification-of-bilinear-transform](https://dsp.stackexchange.com/questions/62752/justification-of-bilinear-transform)  
27. Bilinear transform \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Bilinear\_transform](https://en.wikipedia.org/wiki/Bilinear_transform)  
28. Bilinear Transform (Tustin's Method) applied to the Derivative, accessed September 30, 2025, [https://dsp.stackexchange.com/questions/58432/bilinear-transform-tustins-method-applied-to-the-derivative](https://dsp.stackexchange.com/questions/58432/bilinear-transform-tustins-method-applied-to-the-derivative)  
29. Bilinear Transform \- Pieter's Pages, accessed September 30, 2025, [https://tttapa.github.io/Pages/Mathematics/Systems-and-Control-Theory/Digital-filters/Discretization/Bilinear-transform.html](https://tttapa.github.io/Pages/Mathematics/Systems-and-Control-Theory/Digital-filters/Discretization/Bilinear-transform.html)  
30. Inverse Laplace transform \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Inverse\_Laplace\_transform](https://en.wikipedia.org/wiki/Inverse_Laplace_transform)  
31. The Inverse z-Transform Using Contour Integration \- Sec. 4.5, accessed September 30, 2025, [https://course.ece.cmu.edu/\~ece491/lectures/L07/IZT\_ContourIntegration.pdf](https://course.ece.cmu.edu/~ece491/lectures/L07/IZT_ContourIntegration.pdf)  
32. 18.04 S18 Topic 12: Laplace transform \- MIT OpenCourseWare, accessed September 30, 2025, [https://ocw.mit.edu/courses/18-04-complex-variables-with-applications-spring-2018/1b1cbc6540b338b58b7bc1b1cc1f280b\_MIT18\_04S18\_topic12.pdf](https://ocw.mit.edu/courses/18-04-complex-variables-with-applications-spring-2018/1b1cbc6540b338b58b7bc1b1cc1f280b_MIT18_04S18_topic12.pdf)  
33. theory of laplace transforms and their applications, accessed September 30, 2025, [http://math.uchicago.edu/\~may/REU2022/REUPapers/Thiagarajan.pdf](http://math.uchicago.edu/~may/REU2022/REUPapers/Thiagarajan.pdf)  
34. Different proofs of uniqueness of the Laplace transform \- Mathematics Stack Exchange, accessed September 30, 2025, [https://math.stackexchange.com/questions/1179977/different-proofs-of-uniqueness-of-the-laplace-transform](https://math.stackexchange.com/questions/1179977/different-proofs-of-uniqueness-of-the-laplace-transform)  
35. 9.10: The Inverse Laplace Transform \- Mathematics LibreTexts, accessed September 30, 2025, [https://math.libretexts.org/Bookshelves/Differential\_Equations/Introduction\_to\_Partial\_Differential\_Equations\_(Herman)/09%3A\_Transform\_Techniques\_in\_Physics/9.10%3A\_The\_Inverse\_Laplace\_Transform](https://math.libretexts.org/Bookshelves/Differential_Equations/Introduction_to_Partial_Differential_Equations_\(Herman\)/09%3A_Transform_Techniques_in_Physics/9.10%3A_The_Inverse_Laplace_Transform)  
36. 17\. InVERsE LAPlACE TRAnsFoRms This is one more topic to do with contour integration. In this dis \- UCSD Math, accessed September 30, 2025, [https://www.math.ucsd.edu/\~jmckerna/Teaching/19-20/Spring/120B/l\_17.pdf](https://www.math.ucsd.edu/~jmckerna/Teaching/19-20/Spring/120B/l_17.pdf)  
37. Inverse Z-transform \- Coert Vonk, accessed September 30, 2025, [https://coertvonk.com/physics/lfz-transforms/z/inverse-z-transform-22153](https://coertvonk.com/physics/lfz-transforms/z/inverse-z-transform-22153)  
38. 9.9: The Convolution Theorem \- Mathematics LibreTexts, accessed September 30, 2025, [https://math.libretexts.org/Bookshelves/Differential\_Equations/Introduction\_to\_Partial\_Differential\_Equations\_(Herman)/09%3A\_Transform\_Techniques\_in\_Physics/9.09%3A\_The\_Convolution\_Theorem](https://math.libretexts.org/Bookshelves/Differential_Equations/Introduction_to_Partial_Differential_Equations_\(Herman\)/09%3A_Transform_Techniques_in_Physics/9.09%3A_The_Convolution_Theorem)  
39. Convolution theorem \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Convolution\_theorem](https://en.wikipedia.org/wiki/Convolution_theorem)  
40. Laplace Transform Properties \- Linear Physical Systems Analysis, accessed September 30, 2025, [https://lpsa.swarthmore.edu/LaplaceXform/FwdLaplace/LaplaceProps.html](https://lpsa.swarthmore.edu/LaplaceXform/FwdLaplace/LaplaceProps.html)  
41. Differentiation and the Laplace Transform, accessed September 30, 2025, [https://howellkb.uah.edu/public\_html/DEtext/Part4/Laplace\_derivatives.pdf](https://howellkb.uah.edu/public_html/DEtext/Part4/Laplace_derivatives.pdf)  
42. Properties of the Fourier Transform, accessed September 30, 2025, [https://sheffield.ac.uk/media/30846/download?attachment](https://sheffield.ac.uk/media/30846/download?attachment)  
43. Spectral theory \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Spectral\_theory](https://en.wikipedia.org/wiki/Spectral_theory)  
44. accessed September 30, 2025, [https://fiveable.me/key-terms/electrical-circuits-systems-ii/bibo-stability\#:\~:text=How%20does%20BIBO%20stability%20relate,half%20of%20the%20complex%20plane.](https://fiveable.me/key-terms/electrical-circuits-systems-ii/bibo-stability#:~:text=How%20does%20BIBO%20stability%20relate,half%20of%20the%20complex%20plane.)  
45. Routh–Hurwitz stability criterion \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Routh%E2%80%93Hurwitz\_stability\_criterion](https://en.wikipedia.org/wiki/Routh%E2%80%93Hurwitz_stability_criterion)  
46. Jury stability criterion \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Jury\_stability\_criterion](https://en.wikipedia.org/wiki/Jury_stability_criterion)  
47. Jury Stability Test | PDF \- Scribd, accessed September 30, 2025, [https://www.scribd.com/presentation/870007261/Jury-Stability-Test](https://www.scribd.com/presentation/870007261/Jury-Stability-Test)  
48. LAPLACE TRANSFORM AND Z-TRANSFORM: UNIFICATION AND EXTENSION ∗ 1\. Introduction. A time scale is a nonempty closed subset of th \- MST.edu, accessed September 30, 2025, [https://web.mst.edu/\~bohner/papers/ltaztuae.pdf](https://web.mst.edu/~bohner/papers/ltaztuae.pdf)  
49. LAPLACE TRANSFORM AND Z-TRANSFORM: UNIFICATION AND EXTENSION 1\. Introduction A time scale is a closed subset of the reals. In th \- UNL math, accessed September 30, 2025, [https://www.math.unl.edu/\~apeterson1/pub/laplace](https://www.math.unl.edu/~apeterson1/pub/laplace)  
50. Understanding Poles and Zeros 1 System Poles and Zeros \- MIT, accessed September 30, 2025, [https://web.mit.edu/2.14/www/Handouts/PoleZero.pdf](https://web.mit.edu/2.14/www/Handouts/PoleZero.pdf)  
51. Nyquist–Shannon sampling theorem \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon\_sampling\_theorem](https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem)  
52. Aliasing \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Aliasing](https://en.wikipedia.org/wiki/Aliasing)  
53. Aliasing and the Sampling Theorem \- YouTube, accessed September 30, 2025, [https://www.youtube.com/watch?v=7eFGY6JVTnc](https://www.youtube.com/watch?v=7eFGY6JVTnc)  
54. Poisson summation formula \- Wikipedia, accessed September 30, 2025, [https://en.wikipedia.org/wiki/Poisson\_summation\_formula](https://en.wikipedia.org/wiki/Poisson_summation_formula)  
55. (PDF) The sampling theorem, Poisson's summation formula, general Parseval formula, reproducing kernel formula and the Paley-Wiener theorem for bandlimited signals \- their interconnections \- ResearchGate, accessed September 30, 2025, [https://www.researchgate.net/publication/263753346\_The\_sampling\_theorem\_Poisson's\_summation\_formula\_general\_Parseval\_formula\_reproducing\_kernel\_formula\_and\_the\_Paley-Wiener\_theorem\_for\_bandlimited\_signals\_-\_their\_interconnections](https://www.researchgate.net/publication/263753346_The_sampling_theorem_Poisson's_summation_formula_general_Parseval_formula_reproducing_kernel_formula_and_the_Paley-Wiener_theorem_for_bandlimited_signals_-_their_interconnections)  
56. Lecture Notes on Dirac delta function, Fourier transform, Laplace transform, accessed September 30, 2025, [https://materia.dfa.unipd.it/salasnich/dfl/dfl.pdf](https://materia.dfa.unipd.it/salasnich/dfl/dfl.pdf)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAASwAAACWCAYAAABkW7XSAAAEYklEQVR4Xu3UAQkAAAwCwdm/9HI83BLIOdw5AgQIRAQWySkmAQIEzmB5AgIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlAABg+UHCBDICBisTFWCEiBgsPwAAQIZAYOVqUpQAgQMlh8gQCAjYLAyVQlKgIDB8gMECGQEDFamKkEJEDBYfoAAgYyAwcpUJSgBAgbLDxAgkBEwWJmqBCVAwGD5AQIEMgIGK1OVoAQIGCw/QIBARsBgZaoSlACBB1YxAJfjJb2jAAAAAElFTkSuQmCC>