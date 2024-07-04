---
aliases: [FFT, PSD]
---
## Start Date: 2022-12-22

> Category: Note

Tags:
#numerik

Links:
[17.3 FFT in MATLAB(R), Window (Fensterfunktion), Hann - YouTube](https://www.youtube.com/watch?v=7bi5_KC08Kg)

[Comparing the PSD to the Simple Fourier Transform for Vibration - YouTube](https://www.youtube.com/watch?v=tnHWNyruoFg)

>[! Summary]
>

---
# General
The initial data is a set of measured values with a Period $T$. This can be represented as a sum of sin and cosine signals.
$$f(t)=\sum\limits_{n=-\infty}^{\infty}c_{n}e^{2\pi n \frac{t}{T}i}$$

$n$ indicates how high the frequency is comapred to the base frequency
The $\frac{t}{T}$ makes sure that the signal is gridded to full revolutions $(2\pi)$.
$c_{n}$ is Fourier Coefficient that marked the amplitude of the Spektras. In continuous time those would be calculated as follows:

$$c_{n}=\frac{1}{T}\int_{0}^{T}e^{-2\pi n \frac{t}{T} i} f(t) dt$$
For a pure sinusoidal or cosine signal it is necessary to have a $-c_{n}$ for every $c_{n}$. (Euler Formula)
>[!info]+
>$$e^{i\phi}=\cos(\phi)+i\sin(\phi)$$$$\cos(\phi)=Re(e^{i\phi})=\frac{{e^{i\phi}+e^{-i\phi}}}{2}$$
>$$\sin(\phi)=Im(e^{i\phi})=\frac{{e^{i\phi}-e^{-i\phi}}}{2i}$$


>[!Note]- Bsp
>$$f(t)=sin(13\cdot 2\pi \cdot t)$$
>$$f(t)=\sum\limits_{n=-\infty}^{\infty} c_{n}e^{2\pi n \frac{t}{T} i}$$
>$$f(t)=sin(13\cdot 2\pi \cdot t)=\frac{e^{13\cdot 2\pi \cdot t \cdot i}-e^{13\cdot 2\pi \cdot t\cdot  i}}{2 i}=\frac{1}{2i}e^{13\cdot 2\pi \cdot t \cdot i} - \frac{1}{2i}e^{-13\cdot 2\pi \cdot t \cdot i}$$
>$$c_{n1}=\frac{1}{2i}\ ;\ c_{n2}=-\frac{1}{2i}$$
>![[FFT1.png]]


# Windows
The FFT returns the Fourier Coefficients for a signal that contains endless repititions of a sequence. If there is a step between the end of the Sequence and the beginning, that step contains all frequencies and thus coefficients for tecnically "unexisting" frequencies are are include.
![[Pasted image 20230221141806.png]]
![[Pasted image 20230221141925.png]]
To avoid this, a window function can be used. The window function is multiplied with the sequence that is used for the FFT. It blends the beginning and the end to zero and holds the original signal in the middle.
![[Pasted image 20230221143544.png]]

# Getting the right frequencys from fft()
## True Magnitudes
Matlab returns a vector with the Fourier Coefficients that is as long as the number of samples from the original signal.

The magnitudes within this array depend on the number of samples.
$$mag=\frac{mag_{true}}{2}\cdot Fs\cdot L$$
$Fs$ - Number of Samples per Seconde $[\frac{1}{s}]$ 
$L$ - Length of the Sequence $[s]$ 

## True frequencies
As every sinusoid (or cosine) consists of a pair of exponentials. The fft can detect all contained frequencies that are less then half the sampling frequency. (Everything else would just output random values arround zero in the time domain...)

The first tested Frequency is zero then the tested frequencies are counted up until half of the sampling frequency and then from zero down again. So the first half of the array is sufficient to get the relevant frequencies.

>[!Note]+ Example
>For a Signal Sequence that is $2\, s$  long and sampled with a frequency of $10\, Hz$ that contains sinusoids with up to $5\, Hz$.
>$$f(t)=sin(2\pi \cdot 1t)+2sin(2\pi \cdot 2t)+3sin(2\pi \cdot 3t)+4sin(2\pi \cdot 4t)+5sin(2\pi \cdot 5t)$$
>The Time Series looks like this
>![[Pasted image 20230221155034.png]]
>The Number of Samples is $N=Fs\cdot L=20$ and the sampling frequency was $10\, Hz$
>Thus frequencies up to (but not including) $5\, Hz$ can be detected with an accuracy of $0.5\, Hz$
>
>The corresponding array resulting from the fft() function looks like this:
>![[Pasted image 20230221155330.png]]
>picking the right entries and correcting the magnitudes with the formula above the frequency spectrum is revealed.
>![[Pasted image 20230221155509.png]]

# Influences on the Results
 1:  $N$ - Number of  Samples in the Signal Sequence
	The higher the Number of Samples per Sequence, the smaller the steps in the detected frequency range ($dF$ gets smaller)
	As the Term Spectral Lines refers to the number of frequency domain samples:
	A higher number of samples gives more Spectral Lines within the captured Bandwidth.
 2: $Fs$ - The Sampling Frequency
	The highest detectable frequency is $(\frac{Fs}{2})$ but a frequency occuring with half the sample rate would only give zeros and for every frequency that is even higher, the zero-crossings between two samples would be lost wich would result in a falsly detected additional frequency component at lower frequencies (including $\frac{Fs}{2}$).

## First Example - Same Bandwidth with different frequency Resolution

This can be achieved by having the same sampling frequency but changing the size of the window.
![[Pasted image 20230222105830.png]]
The Magnitudes of the resulting Frequency Spectrum change as the Signal gets distributed over more Frequencies. (The total of the Magnitudes stays the same!)
![[Pasted image 20230222105949.png]]

## Example 2 - Different Bandwidth with the same frequency Resolution
This can be achieved by changing the sampling frequency but keeping the window size constant.
![[Pasted image 20230222111103.png]]
This leads to the first fft() not beeing able to detect the frequency component at $30\, Hz$ 
![[Pasted image 20230222111226.png]]


# PSD
[What is a Power Spectral Density (PSD) - Siemens Course](https://community.sw.siemens.com/s/article/what-is-a-power-spectral-density-psd#:~:text=Power%20Spectral%20Density%20(PSD)%20normalizes,similar%20appearance%20(Picture%207).&text=The%20term%20%E2%80%9Cnormalizing%E2%80%9D%20by%20the,line%20by%20the%20frequency%20resolution)

The amplitude of the PSD is normalized by the spectral resolution employed to digitize the signal.

In a Autopower Spectrum (discussed in the above section) only Magnitude and Frequency of the Signal are shown. But as the frequency resolution ($\Delta F$) gets finer, the same signal is being divided into smaller parts (the total remains the same, but the magnitudes change)

Power Spectral Density (PSD) normalizes the amplitudes by the frequency resolution to give the amplitudes a similar appearance.

![[PSD.png]]

## PSD for White Noise
```Matlab
[pxx,pf]=pspectrum(u,Fs,'power');
pNorm=10*log(pxx);

figure;
stem(pf/max(pf),pNorm,'BaseValue',mean(pNorm))
xlabel(append('Normalized Frequency (Bandwidth: ', string(max(f)), ' Hz)'));
ylabel('10log_{10}(Mag / (\DeltaF\cdotL))')
title(append('PSD \DeltaF=', string(dF),' Hz'));
legend('fft','pspectrum','Location','southoutside')
grid on
if dark==1
    plot_darkmode
end

```

## Spectral Power Density as Concept
[[@(miller2004)_Probability and random processes_ With applications to signal processing and communications|miller2004]]
The random process is time variant and we can only calculate a portion of the signal and define it as periodically recurring sequence.
$$X_{t_{0}}(t)=\left\{\begin{array}{c}
X(t)&|t|\leq t_{0} \\ 0&|t| > t_0
\end{array} \right\}$$
The Energy in this random process is
$$E_{X_{t_{0}}}=\int_{-t_0}^{t_{0}}X^{2}(t)dt=\int_{-\infty}^{\infty}X^{2}_{t_0}(t)dt$$

and the time averaged power is
$$P_{X_{t_{0}}}=\frac{1}{2t_{0}}\int_{-\infty}^{\infty}X_{t_{0}}^{2}(t)dt=\frac{1}{2t_{0}}\int_{-\infty}^{\infty}|X_{t_{0}}(f)|^2df$$

[PowerSpectralDensity.ppt (utk.edu)](http://web.eecs.utk.edu/~mjr/ECE504/PresentationSlides/PowerSpectralDensity.pdf)

