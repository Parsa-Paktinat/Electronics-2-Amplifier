# Electronics-2-Amplifier

## Overview

Electronics-2-Amplifier documents a two-phase project designed and evaluated entirely in **LTspice**. The repository includes circuit schematics, AC and transient simulation plots, audio-related transient waveforms, and the project reports.

- **Phase 1** centers on a **very high-gain open-loop amplifier** that meets the project's Phase 1 specifications (high differential gain, high CMRR, wide output swing, and a specified load).
- **Phase 2** centers on **closing the loop**: adding a power output stage capable of driving a low-impedance load and applying **global negative feedback** to set a stable closed-loop gain.

> **Note:** Phase 1 targets and Phase 2 results are separate design goals and should not be conflated. The performance figures reported here come from the respective phase reports; only Phase 2 closed-loop results are summarized numerically in this README.

## Phase 1 — High-Gain Open-Loop Amplifier

Phase 1 targets an open-loop amplifier with very high differential gain (well above the required > 54 dB), high CMRR, and wide output swing from a ±10 V supply, designed around a **1 mV input** and a **500 Ω load**.

The reported Phase 1 design uses:

- A **MOSFET folded-cascode differential input stage**, chosen for its high differential gain, low common-mode gain, and convenient control of the first-stage output operating point;
- A **cascoded current-mirror load**, which provides a high-impedance active load for maximum gain (at the cost of more delicate bias-point tuning);
- A **source-degenerated common-source gain stage** as the second stage, whose source degeneration linearizes the stage and helps set the overall gain;
- An **output buffer** that isolates the high-impedance gain stages from the load and protects the output swing.

Biasing throughout is arranged with current references and multiple current mirrors, and active loads are preferred over resistors for gain and cost reasons.

> The supplied [`reports/phase2_report.pdf`](reports/phase2_report.pdf) is a **partly filled Phase 1 report** (it already contains the Phase 1 design narrative and results), not a blank course template. No additional unverified Phase 1 numerical results are asserted in this README; see the report itself for the detailed figures.

## Phase 2 — Output Stage, Biasing, and Global Negative Feedback

Phase 2 extends the Phase 1 amplifier so it can drive a **50 Ω load**, by adding:

- A **complementary BJT push-pull output stage**, arranged as **Darlington pairs** to reduce the loading of the output swing on the limited output-stage bias current;
- **Diode-connected BJT biasing** in the bases of the output transistors (since discrete diodes were not permitted), sourced from the Phase 1 current-reference branch, to establish a small quiescent bias and **reduce crossover distortion**;
- **Global negative feedback**, taken from the output node and returned in series to the differential input stage, which sets a predictable closed-loop gain, lowers output impedance, and improves linearity.

For the closed-loop design, the feedback network uses **Rg = 10 kΩ** and **Rf = 190 kΩ**, giving a nominal closed-loop gain of approximately **20 V/V** (1 + Rf/Rg). These values are **LTspice simulation / report values**, not hardware measurements.

The Phase 2 report ([`reports/phase2_report.pdf`](reports/phase2_report.pdf)) documents the resulting closed-loop performance against the Phase 2 requirements (closed-loop gain, output swing, efficiency, THD, PSRR, and cost budget). Please consult the report for those numbers rather than inferring Phase 1 performance from the open-loop plots below.

## Circuit Architecture

The circuit schematic is provided as an LTspice circuit image:

![LTspice circuit schematic](assets/schematic_overview.png)

## Simulation Results

The plots below are results from LTspice simulations:

### AC response

The AC analysis plot shows approximately 1 V AC at the input and 20 V AC at the output, corresponding to an approximate voltage gain of **20 V/V** under the displayed plot conditions.

![AC response plot](assets/ac_response.png)

### Transient response

The transient waveform shows a 50 mV input and an output amplitude of approximately 8 V.

![Transient response plot](assets/transient_response.png)

Exact amplitude definitions (for example, peak, peak-to-peak, or RMS) depend on the plot measurement conventions; the values above are stated as presented and should not be interpreted as a more specific measurement than the plots establish.

## Audio Demonstration

The following two waveforms are transient-simulation waveforms for the input audio and output audio:

![Input and output audio waveforms](assets/audio_waveform_1.png)

![Input and output audio waveforms](assets/audio_waveform_2.png)

Audio files:

- [Input audio](audio/audio_input.wav)
- [Output audio](audio/audio_output.wav)

## Repository Structure

```text
Electronics-2-Amplifier/
│
├── README.md
│
├── simulation/
│   ├── phase1_differential_amplifier.asc
│   └── phase2_closed_loop_amplifier.asc
│
├── reports/
│   ├── phase1_report.pdf
│   └── phase2_report.pdf
│
├── audio/
│   ├── audio_input.wav
│   └── audio_output.wav
│
└── assets/
    ├── schematic_overview.png
    ├── ac_response.png
    ├── transient_response.png
    ├── audio_waveform_1.png
    └── audio_waveform_2.png
```

## Tools

- **LTspice** — circuit schematic and simulation plots (AC and transient analyses).

## References

- Phase 1 report: [`reports/phase1_report.pdf`](reports/phase1_report.pdf)
- Phase 2 report: [`reports/phase2_report.pdf`](reports/phase2_report.pdf)

## Notes

- All reported circuit results are from **LTspice simulations**, not presented as hardware measurements.
- Values (including Rg, Rf, and the ~20 V/V closed-loop gain) are approximate and should be read in the context of the displayed plots and their measurement conventions.
- Phase 1 open-loop targets and Phase 2 closed-loop results are distinct and should not be compared directly.
- No additional performance metrics are asserted here; see the two referenced reports for full details.
