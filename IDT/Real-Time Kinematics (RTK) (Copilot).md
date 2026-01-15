Real-Time Kinematics (RTK) is a differential GNSS technique that uses carrier-phase measurements and correction data from a fixed base station to deliver centimeter-level positioning accuracy in real time.

---

## How RTK Works

1. A **base station** at a known location tracks GNSS satellites and computes both code and carrier‐phase measurements.
2. The base broadcasts these raw observations and its precise coordinates to one or more **rovers** via a real-time link (radio, cellular, etc.).
3. Each rover compares its own carrier-phase measurements with the base’s data to cancel out common errors—satellite clock bias, orbital errors, atmospheric delays.
4. By resolving the integer “cycle ambiguities” in the carrier phase, the rover reconstructs the precise range to each satellite, yielding positions with centimeter precision.

---

## Performance and Limitations

- **Accuracy**: typically 1–3 cm horizontally and 2–5 cm vertically within 10–20 km of the base.
- **Convergence Time**: initial ambiguity fixing can take seconds to minutes, depending on signal quality and baseline length.
- **Range**: effective up to ~20 km from the base; beyond that, unmodeled atmospheric differences degrade accuracy.
- **Communication**: requires a constant, low-latency link (e.g., UHF/VHF radio, cellular, or internet) between base and rover.

---

## Common Applications

- Land and hydrographic surveying
- Precision agriculture (automated steering)
- Construction site machine control
- Unmanned vehicle and drone navigation
- GIS data collection and mapping

---

## Beyond Basic RTK

You might also explore:

- **Network RTK**: leverages multiple base stations and Virtual Reference Stations (VRS) to expand coverage and reduce baseline-dependent errors.
- **PPP-RTK**: combines Precise Point Positioning (PPP) with RTK corrections for global centimeter-level accuracy without a local base.
- **NTRIP Protocol**: an internet-based standard for streaming GNSS corrections.

Are you looking at a specific hardware setup, software solution, or application scenario? Let me know, and I can dive deeper into how to implement and optimize RTK for your needs.