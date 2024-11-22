---
layout: ../../layouts/project.astro
title: "Optimizing Motion Systems"
description: Unleashing Peak Performance in the Fourth-Order Motion (PATO) Control System
image: ""
dateFormatted: Oct 1st, 2024
---

**Objective:**

This experiment focuses on optimizing the performance of a fourth-order Passive All-Pass Transmittance Operator (PATO) system. The system includes components such as a load-side encoder, load-side rotating mass, spring, motor-side rotating mass, and motor-side encoder. The aim is to control the non-co-located mass with precision along a predefined bidirectional trajectory, simulating real-time control scenarios.

Accurate positioning of the non-co-located mass is critical, while maintaining minimal tracking errors and minimizing the total time for the motion. The co-located mass, at the motor side, directly benefits from torque application and angular displacement measurement via the encoder.

The experiment imposes key constraints to ensure robust performance. The scanning stroke must span 120 radians, covering at least 19.1 revolutions in both forward and backward directions. The total stroke is limited to 125 radians, leaving only 2.5 radians for turn-around motion at each end. To address production variations and uncertainties, the feedback loop's modulus margin is capped at 6 dB. Additionally, the control system operates at a sampling rate of no more than 4 kHz.

This setup seeks to emulate practical applications, ensuring the system performs reliably under stringent requirements while achieving high precision and efficiency.  
<br/>**System identification:**

The transfer functions for the co-located and non-co-located masses are given by \\autoref{eq: EoM (1)} and \\autoref{eq: EoM (2)}, respectively \\cite{course_slides2}.

![A diagram of a cylinder



\\begin{equation}\\label{eq: EoM (1)}

\\frac{\\theta_1}{T_e} = \\frac{J_2 s^2 + d_rs + k_r}{J_1 J_2 s^4 + (J_1 + J_2) d_rs^3 + (J_1 + J_2) k_rs^2}

\\end{equation}

\\begin{equation}\\label{eq: EoM (2)}

\\frac{\\theta_2}{T_e} = \\frac{d_rs + k_r}{J_1 J_2 s^4 + (J_1 + J_2) d_rs^3 + (J_1 + J_2) k_rs^2}

\\end{equation}  
<br/><br/>Given the marginal stability of the open loop system for both co-located and non-co-located masses, we can measure the system by using the \\textit{Direct method} to obtain the magnitude and phase spectrum of the PATO-system. If the system was not open-loop stable, we had to use \\textit{Indirect method} to measure the FRF. Therefore, the following block diagram is used parallel to signal processing to derive the plant's FRF,  
<br/><br/>By employing \\textit{White Noise}, the correlation between noise and input can be eliminated as long as the signals are sufficiently averaged. This can lead to a more accurate estimation of the system's transfer function. But, a downside is that it can have potential issues like noise sensitivity and the need for careful experimental design. Thus, by multiplying the equation that relates the output signal to the input signal by the conjugate of the input signal, which approaches zero. As a result, the plant's transfer function $H(f)$ can be expressed in \\autoref{eq:H_f}:

\\begin{equation}\\label{eq:H_f}

H(f) \\approx \\frac{S_{yu}(f)}{S_{uu}(f)}

\\end{equation}

![A diagram of a waveform



**Coherence**

During testing, it was observed that the motor and load encoders rotated in opposite directions, causing the phase to start at 0∘0^\\circ instead of the expected ±180∘\\pm 180^\\circ. This anomaly shifted the Nyquist plot to the first quadrant. Multiplying the load measurements by −1 corrected the 2 slope, relocating the Nyquist plot to the third quadrant. From the frequency response function (FRF) measurements, the magnitude and phase spectra were plotted, revealing a resonance peak at 57.4 Hz for both co-located and non-co-located masses. The co-located mass's resonance at 1 kHz, linked to motor dynamics, is irrelevant to the primary objective.

![A graph of a graph



When coherence is low, the reliability of data from the PATO setup decreases, as it indicates weak correlation between input and output signals. High coherence (>0.8>0.8) reflects strong frequency-domain correlation, enhancing reliability. As shown in \\autoref{fig:coherencevariance}, coherence below 10 Hz is low, suggesting poor representation of the system’s dynamics. Between 10 Hz and the resonance frequency of 57.4 Hz, coherence improves, providing a better depiction of the setup’s motion. Beyond 57.4 Hz, coherence rapidly declines.

The frame size (\\textit{nfft}) significantly affects coherence levels and resolution. Using a sampling rate of 4 kHz over 75 seconds (300,000 samples), the best coherence was achieved with a frame size of 12,000 samples, a variance of 0.3, and an overlap of 6,000 samples, resulting in 49 averaged frames. Adjusting the frame size impacted resolution and averaging. Smaller frame sizes reduced resolution, while larger sizes improved resolution but limited disturbance reduction. Optimizing frame size balanced resolution and averaging, improving data reliability and clarity in the frequency domain.

<br/>**Feedback controller**

A feedback controller was designed with a high bandwidth to meet the stability margins of the PATO setup. The objective was to achieve a consistent −2-2 slope before and −4-4 slope after the resonance for stable dynamics and accurate reference tracking. A lead-lag block introduced positive phase and low-frequency gain, extending the bandwidth to 14.5 Hz. A low-pass filter above 100 Hz attenuated noise, while a notch filter at 57.6 Hz suppressed resonance effects. This controller reduced the error range to 0.17–40 mrad, but the results were insufficient, requiring advanced techniques for improved tracking precision.

![A graph showing a error


<br/>Need for feedforward and feedforward controller:

The feed-forward model begins with a third-order motion profile, incorporating reference position, velocity, acceleration, and jerk to ensure smooth transitions between acceleration phases. This simplified model captures the key forces affecting the system's motion.

A low-bandwidth controller with 2.61 Hz bandwidth, modulus margin of 5.7 dB, gain margin of 7.9 dB, and phase margin of 42.8∘42.8^\\circ42.8∘ is employed to tune the feed-forward parameters. This approach ensures basic stability and provides insights into the system's dynamics. By iteratively adjusting parameters and analyzing error profiles, the controller improves responsiveness, reduces errors, and enhances reference tracking. Supporting factors are outlined in \\autoref{tab:lbw_controller}.

**Feedforward reference traj**

As shown in \\autoref{fig:referencetrajectory_high}, parameters were set for a trajectory of 300 rad in 6 seconds, with a velocity of 120 rad/s and acceleration of 180 rad/s², corresponding to a base frequency of 0.16 Hz (16\\frac{1}{6} s). The controller's low sensitivity magnitude at this frequency minimized resulting errors, as illustrated in \\autoref{fig:s_plot}. To test performance at a higher base frequency, a more challenging trajectory of 120 rad in 3 seconds was introduced, maintaining the same velocity and acceleration profiles. This raised the base frequency to 0.33 Hz (13\\frac{1}{3} s), where error reduction was less effective compared to the initial trajectory.

![A graph of a function



As shown in \\autoref{fig:ff_tuned}, the error profile improves progressively at each tuning stage. Initially, tuning KfcK_{fc} significantly reduces the error magnitude. Subsequently, KfcK_{fc} is further adjusted to eliminate the error slope entirely. Finally, KfaK_{fa} is tuned to optimize the acceleration component. Once these parameters are optimized, the error is effectively removed, with the final tuned values provided in \\autoref{tab:ff_tuning}.

![A graph of a graph showing different colored lines



Feedforward model:

After fine-tuning the feed-forward model to neutralize system dynamics and improve reference tracking with a low-bandwidth controller, implementing a high-bandwidth controller further enhances performance. A feedback controller with a bandwidth of 12.6 Hz is introduced to minimize errors more effectively. High-bandwidth controllers respond faster to reference changes and disturbances, allowing precise tracking of high-frequency components essential for accurate bi-directional positioning. This controller uses the same building blocks outlined in \\autoref{tab:lbw_controller} but incorporates two additional notch filters with updated coefficients, as detailed in \\autoref{tab:hbw_controller}.

![A graph of a graph showing a position and acceleration



The reference trajectory completes 19 revolutions in one direction before reversing, with an acceleration of 199 rad/s² reaching a velocity of 26.04 rad/s within the first 5 rad. The system maintains this velocity before sharply decelerating, completing half a cycle within 5 seconds (\\autoref{tab:regions}).

The high-bandwidth controller has bandwidth of $12.61$ \[Hz\] and Modulus Margin of $6$ \[dB\] with Gain Margin of $7.45$ \[dB\] and Phase Margin as \\(36.8^\\circ\\).

The notch filter is used to nullify the resonance that is created by the system's dynamics. The idea is to get a smooth $-2$ magnitude slope such that the dynamics is controlled and reference tracking is quite good over all frequencies. More details can be found in \\autoref{subsec:seventh} about sensitivity where we are able to see the system responses at all the frequencies.



In \\autoref{fig:nyquist_closedloop}, the green curve represents the plant, the blue shows the stable high-bandwidth controller, and the red highlights the controller with double-notch filters. Adding lead-lag blocks and notch filters stabilizes the plant, mitigates resonance, and improves reference tracking stability and accuracy.

Sensitivity :

The sensitivity ($|S(j\\omega)|$) of the PATO-setup can be determined by measuring for performance. It defines the robustness of the system (e.g. the closeness to instability) and determines the resulting closed-loop error \\cite{course_slides1}. To keep in mind is that, a small $|S(j\\omega)|$ can still yield instability, and a large $|S(j\\omega)|$ can still come with stability \\cite{course_slides1}. The sensitivity is determined by the \\textit{Error e} resulting from an \\textit{Input r} as depicted in \\autoref{fig:s_blockdiagram} \\cite{textbook1}.

For the PATO-setup we can plot the sensitivity function, which is shown in \\autoref{fig:s_plot}. Observed can be the Modulus Margin which is the reciprocal of peak sensitivity $|S(j\\omega)\_{\\text{max}}|$. The green curve is the plant itself, and the red curve is the final controller sensitivity with a notch at $4.145$ \[Hz\].

![A graph of a function



Experimental results

In experiment X \\cite{course_slides1}, the reference trajectory was applied to the plant using feedback and feed-forward controllers to meet the criteria: an RMS error below 6 mrad and a peak error below 12 mrad within 12 seconds (\\autoref{tab:regions}).

![A graph showing a number of blue and white bars



Initially, the RMS error was 7.4 mrad, and the peak error reached 18.28 mrad during constant velocity, as shown in \\autoref{fig:before_notch}. The error exhibited periodic motion, confirmed by a dominant frequency at 4.145 Hz in the PSD and CPSD plots (\\autoref{fig:CPSD}). To address this, an inverse notch filter was added, reducing sensitivity at this frequency. The updated RMS error dropped to 2.3764 mrad, and the peak error to 6.2832 mrad (\\autoref{fig:enter-label}).

![A bar code with numbers



Conclusion:

The dynamics of the fourth-order PATO setup were initially approximated using the direct method, with the system's frequency response obtained from both encoders. Optimal noise variance and frame size configurations were determined based on coherence, identifying the most reliable frequency range.

To simplify control, the non-co-located mass encoder was used to track the reference. A feed-forward controller with a 2.6 Hz bandwidth was designed, revealing minimal impact from viscous friction (1⋅10−51 \\cdot 10^{-5}). Tuning identified gain values Kfa=0.00039K_{fa} = 0.00039 and Kfc=0.0075K_{fc} = 0.0075, reducing total error by a factor of three. Subsequently, a feedback controller with a 12.6 Hz bandwidth, incorporating lead-lag and notch filters, enhanced tracking performance.

Error analysis via PSD and CPSD identified recurring errors at the mass rotation frequency. An inverse notch filter effectively attenuated this error, achieving optimal performance within 10 seconds.

In conclusion, the designed controller ensures the PATO setup achieves minimal error and optimal performance for Region 3 (\\autoref{sec:first}).