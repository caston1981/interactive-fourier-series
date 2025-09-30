# Interactive Fourier Series Foundations

An interactive educational web application exploring the mathematical foundations of Fourier Series through visual demonstrations and rigorous theoretical explanations.

![Fourier Series](https://img.shields.io/badge/Mathematics-Fourier%20Analysis-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow)
![Chart.js](https://img.shields.io/badge/Chart.js-Interactive%20Visualizations-orange)

## 🎯 Overview

This application provides a comprehensive visual guide to Fourier Series theory, bridging the gap between abstract mathematical concepts and intuitive understanding. Built for students, researchers, and enthusiasts interested in harmonic analysis and signal processing.

## 📚 Educational Content

### Navigation Sections

- **🏛️ Historical Foundations**: The 19th-century mathematical crisis sparked by Fourier's bold claims
- **📐 Foundational Theory**: Hilbert space $\mathcal{L}^2(\mathbb{T})$ and orthonormal bases
- **🔄 Convergence & Gibbs Phenomenon**: Dirichlet vs. Cesàro summation methods
- **📊 Coefficient Properties**: How function smoothness determines coefficient decay rates
- **🔮 Complex Spectral Geometry**: Complex coefficients $c_n$ in the frequency domain
- **📏 Signal Quality (THD)**: Total Harmonic Distortion and Parseval's identity
- **🌊 Classic Waveforms**: Square, triangle, and sawtooth wave Fourier decompositions
- **🔗 Broader Connections**: Links to Fourier transforms, PDEs, and abstract harmonic analysis

## 🎮 Interactive Features

### Visual Demonstrations

- **Real-time Chart Updates**: Interactive sliders control the number of Fourier terms
- **Multiple Summation Methods**: Compare Dirichlet and Cesàro convergence
- **Function Comparison**: Switch between discontinuous, continuous, and smooth functions
- **Complex Plane Visualization**: Scatter plot showing complex Fourier coefficients
- **Waveform Selection**: Explore different periodic functions and their spectra

### Mathematical Rigor

- **LaTeX Rendering**: All mathematical expressions rendered with MathJax
- **Theoretical Depth**: Graduate-level explanations with proper citations
- **Visual-Conceptual Links**: Connects time-domain shapes to frequency-domain spectra

## 🛠️ Technical Implementation

### Technologies Used

- **Frontend**: HTML5, CSS3, JavaScript ES6+
- **Styling**: Tailwind CSS for responsive design
- **Visualization**: Chart.js for interactive charts and plots
- **Mathematics**: MathJax for LaTeX rendering
- **Typography**: Google Fonts (Inter & Lora)

### Key Components

```javascript
// Core mathematical functions
function fourierSquare(x, N)     // Square wave Fourier series
function fourierTriangle(x, N)   // Triangle wave approximation
function fourierSawtooth(x, N)   // Sawtooth wave synthesis

// Interactive chart systems
setupGibbsChart()               // Convergence demonstration
setupCoefficientsChart()        // Smoothness-decay relationship
setupComplexCoefficientsChart() // Complex plane visualization
setupExampleChart()             // Waveform comparison
```

### Architecture

- **Single-Page Application**: Navigation-based content switching
- **Modular Chart Initialization**: Charts load on-demand for performance
- **Responsive Design**: Mobile-friendly layout with Tailwind CSS
- **Mathematical Accuracy**: Precise coefficient calculations and convergence demonstrations

## 🚀 Getting Started

### Prerequisites

- Modern web browser with JavaScript enabled
- Internet connection for CDN resources (Chart.js, MathJax, Tailwind CSS)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/caston1981/interactive-fourier-series.git
   cd interactive-fourier-series
   ```

2. **Open in browser**
   ```bash
   # Using Python (recommended)
   python3 -m http.server 8000
   # Then visit: http://localhost:8000

   # Or simply open index.html in your browser
   ```

3. **Navigate through sections** using the sidebar menu

## 📖 Learning Path

### Beginner Level
1. Start with **Foundational Theory** for basic concepts
2. Explore **Classic Waveforms** to see Fourier series in action
3. Try the **Coefficient Properties** section to understand smoothness relationships

### Intermediate Level
1. Dive into **Convergence & Gibbs Phenomenon** for convergence theory
2. Study **Complex Spectral Geometry** for frequency domain concepts
3. Learn about **Signal Quality (THD)** and Parseval's identity

### Advanced Level
1. Explore **Historical Foundations** for mathematical context
2. Connect to broader theory in **Broader Connections**
3. Experiment with different summation methods and convergence behaviors

## 🎯 Educational Goals

- **Conceptual Understanding**: Bridge intuition and mathematical rigor
- **Visual Learning**: Connect abstract theory to concrete visualizations
- **Interactive Exploration**: Encourage experimentation and discovery
- **Mathematical Depth**: Provide graduate-level content with proper foundations

## 🤝 Contributing

Contributions welcome! Areas for improvement:

- Additional waveform examples
- More convergence demonstrations
- Enhanced mathematical visualizations
- Accessibility improvements
- Performance optimizations

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Chart.js](https://www.chartjs.org/) for visualizations
- Mathematical rendering powered by [MathJax](https://www.mathjax.org/)
- Styled with [Tailwind CSS](https://tailwindcss.com/)
- Inspired by the rich history of Fourier analysis

## 📚 References

The application includes citations to key mathematical works and theorems throughout the content, providing a foundation for further reading in harmonic analysis and functional analysis.

---

**Explore the fascinating world of Fourier Series - where mathematics meets visualization!** 🌟</content>
<parameter name="filePath">/home/chris/interactive-fourier-series/README.md
