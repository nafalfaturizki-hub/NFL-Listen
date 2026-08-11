# NFL: Nafal Faturizki Listener

**Open Architecture for Affordable Hearing Assistance**

> "Hearing is free and a right for everyone."

NFL is an open-source platform designed to democratize hearing assistance technology. It provides an open, modular architecture that enables anyone to build, repair, and customize hearing assistance devices using commodity components and vendor-independent design.

---

## 🎯 Mission

To eliminate cost and technology dependency as barriers to accessing hearing assistance by creating a transparent, repairable, and affordable open-source ecosystem.

**Our Goal:**
> "Useful hearing assistance devices can be built with open technology, low cost, and without dependency on cloud services or proprietary vendors."

---

## 🌟 Core Principles

- **Open Source** — Firmware and software under GPL-3.0
- **Open Hardware** — Designs under CERN-OHL-S v2
- **Vendor-Independent** — Works with multiple microcontrollers and components
- **Offline-First** — No mandatory cloud, subscription, or internet required
- **Privacy-First** — Audio processing happens on-device
- **Repairable** — Full documentation for diagnosis, repair, and calibration
- **Low-Cost** — Designed for affordability and accessibility
- **Modular** — Flexible DSP pipeline; simple or advanced configurations
- **Rust-Based** — Memory-safe, deterministic, bare-metal capable
- **Reproducible** — Tested and validated with objective metrics

---

## 🏗️ Architecture

NFL is not locked to a single microcontroller or vendor. It uses a layered architecture that allows different hardware implementations while maintaining software compatibility.

```
┌──────────────────────────────────────────┐
│         NFL USER LAYER                   │
│  Audiogram • Profiles • Presets • Safety │
├──────────────────────────────────────────┤
│         NFL DSP CORE                     │
│  EQ • WDRC • Noise Reduction • Feedback  │
│  Limiter • Gain • Frequency Shaping      │
├──────────────────────────────────────────┤
│       NFL AUDIO RUNTIME                  │
│  Buffer • DMA • Scheduling • Clock       │
├──────────────────────────────────────────┤
│   HARDWARE ABSTRACTION LAYER             │
│  Audio • Storage • Radio • Power         │
├──────────────────────────────────────────┤
│           HARDWARE                       │
│  MCU • ADC/DAC • Mic • Amp • Receiver    │
└──────────────────────────────────────────┘
```

### Hardware Flexibility

Implementations can use:
- **Entry-level**: Low-cost MCU for basic amplification
- **Mobile**: MCU with BLE connectivity
- **Advanced**: Powerful hardware for complex DSP algorithms

---

## 🎧 Audio Processing Pipeline

The core of NFL is real-time digital signal processing (DSP):

```
Microphone
    ↓
Audio Capture
    ↓
Input Conditioning
    ↓
Frequency Shaping / EQ
    ↓
Multi-band WDRC
    ↓
Noise Reduction
    ↓
Feedback Control
    ↓
Gain & MPO Limiting
    ↓
Audio Output
    ↓
Receiver
```

Each processing block is designed as an independent module:
- Simple implementations use minimal DSP
- Advanced hardware can employ sophisticated algorithms
- Algorithms are testable on desktop before deployment

---

## 🧠 Technology Stack

### Firmware & DSP
- **Language**: Rust
- **Benefits**:
  - Memory safety without garbage collection
  - Deterministic execution for real-time processing
  - Bare-metal capable for resource-constrained devices
  - Modular and testable design
  - Reproducible builds

### Validation Pipeline
```
WAV File Input
    ↓
NFL DSP Processing
    ↓
Processed Output
    ├── Latency analysis
    ├── SNR analysis
    ├── Frequency response
    ├── THD analysis
    └── Speech quality metrics
```

The same DSP code runs on both desktop simulation and embedded devices.

---

## 👤 Personal Hearing Profiles

User hearing profiles are decoupled from hardware, enabling:

- **Profile Portability**: Use the same hearing profile across multiple NFL devices
- **Consistent Configuration**: Audiogram, frequency response, WDRC parameters, noise reduction settings
- **Hardware Independence**: Switch devices without reconfiguration
- **Separate Calibration**: Individual compensation for microphone, DAC, amplifier, and receiver characteristics

```
Hearing Profile
├── Audiogram
├── Frequency response curve
├── Band-specific gain
├── WDRC parameters
├── Noise reduction settings
├── Feedback control parameters
├── Maximum power output (MPO)
├── Environment presets
└── Calibration metadata
```

---

## 🔬 Testing & Validation

NFL uses objective, measurable benchmarks rather than subjective claims.

### Validation Stages

1. **Simulation** — Desktop algorithm testing with metrics
2. **Electronic Benchmark** — Component-level verification
3. **Acoustic Validation** — Real-world performance testing

### Measured Metrics

- CPU utilization & memory usage
- Processing latency
- Power consumption
- Frequency response
- Noise floor
- Total Harmonic Distortion (THD+N)
- Dynamic range
- Feedback margin
- Speech intelligibility

---

## 🔐 Privacy & Security

### Privacy by Design

- **On-Device Processing**: Audio processing happens locally
- **No Cloud Required**: No mandatory cloud accounts or servers
- **No Forced Uploads**: Audio is never uploaded without explicit consent
- **No Mandatory Analytics**: No behavioral tracking
- **No Subscription**: Optional services, not required for basic functionality

### Optional Connectivity

When smartphone connectivity is used, it's limited to:
- Device configuration
- Calibration procedures
- Hearing profile management
- Diagnostics
- Firmware updates

---

## 🔧 Repairability & Sustainability

Full project documentation includes:

```
Hardware Documentation
├── Schematics
├── PCB source files
├── Gerber files
├── Bill of Materials (BOM)
├── Mechanical design

Firmware & Software
├── Source code
├── Build procedures
├── Testing procedures

Maintenance
├── Repair procedures
├── Calibration procedures
├── Diagnostics guide
├── Assembly documentation
```

### Repair Cycle

```
Device Failure
    ↓
Diagnosis (documented)
    ↓
Component Replacement (available)
    ↓
Calibration (documented)
    ↓
Reuse

NOT:

Device Failure
    ↓
Discard
    ↓
Buy New
```

---

## 🌱 Open Ecosystem

NFL can be developed and deployed by:

- **Engineers & Students**: Hobbyist and academic implementations
- **Technical Schools & Universities**: Educational projects and prototypes
- **Maker Communities**: DIY hearing assistance devices
- **NGOs & Social Organizations**: Community-driven accessibility programs
- **Local Technicians**: Service and repair networks
- **Small Manufacturers**: Cost-effective production runs

### Scaling Options

**NFL Basic**
- Ultra-low-cost entry-level device
- Essential amplification and noise reduction

**NFL Advanced**
- Complex DSP algorithms
- Enhanced signal processing
- Advanced features

Both remain part of the same ecosystem when following NFL specifications.

---

## 📋 Project Structure

```
nfl/
├── firmware/           # Rust-based firmware (GPL-3.0)
├── dsp/                # Audio processing algorithms (GPL-3.0)
├── hardware/           # PCB designs and schematics (CERN-OHL-S v2)
├── software/           # Desktop tools and utilities
├── documentation/      # Complete build and usage guides (CC BY-SA 4.0)
├── tests/              # Validation and benchmark tests
├── simulator/          # Desktop DSP simulator
└── README.md          # This file
```

---

## 📜 Licensing

| Component | License |
|-----------|---------|
| Firmware | GPL-3.0 |
| Software & DSP | GPL-3.0 |
| Hardware Design | CERN-OHL-S v2 |
| Documentation | CC BY-SA 4.0 |

Each component includes build and usage documentation to ensure the community is not dependent on the original creators' personal knowledge.

---

## 🚀 Getting Started

### Prerequisites
- Rust toolchain (latest stable)
- Hardware components (see BOM in `/hardware`)
- Basic embedded systems knowledge

### Quick Start

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-org/nfl.git
   cd nfl
   ```

2. **Build the Simulator**
   ```bash
   cd simulator
   cargo build --release
   ```

3. **Run Tests**
   ```bash
   cargo test --all
   ```

4. **Review Hardware Documentation**
   ```
   See /hardware/README.md for PCB assembly and testing
   ```

For detailed build and deployment instructions, see [BUILDING.md](./BUILDING.md).

---

## 🤝 Contributing

We welcome contributions from:
- DSP algorithm improvements
- Hardware reference designs
- Documentation and translations
- Testing and validation
- Community adaptations

Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 📚 Documentation

- **[Architecture Guide](./docs/ARCHITECTURE.md)** — System design and specifications
- **[Hardware Guide](./hardware/README.md)** — Component selection and PCB assembly
- **[Firmware Guide](./firmware/README.md)** — Compilation and deployment
- **[DSP Reference](./dsp/README.md)** — Algorithm documentation
- **[User Manual](./docs/USER_MANUAL.md)** — Operation and configuration

---

## ❤️ Philosophy

NFL is founded on a simple belief:

> "Hearing assistance is not a luxury."

Millions of people live with hearing limitations while the technology to help them already exists. The barrier is often not the technology itself—it's **access**.

NFL works to reduce that barrier through open technology.

**Not to defeat the industry.**  
**Not to force everyone onto one device.**  
**But to create a foundation anyone can use to build their own solution.**

---

## 📞 Community & Support

- **Issues**: [GitHub Issues](https://github.com/your-org/nfl/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/nfl/discussions)
- **Email**: contact@nfl-project.org
- **Forum**: [Community Forum](https://forum.nfl-project.org)

---

## 📊 In One Sentence

**NFL is an open-source and open-hardware platform for building affordable, modular, repairable, privacy-first hearing assistance devices without vendor lock-in.**

---

## 📝 Citation

If you reference NFL in academic or professional work, please cite as:

```
@software{nfl2024,
  title={NFL: Nafal Faturizki Listener - Open Architecture for Affordable Hearing Assistance},
  author={[Your Organization]},
  year={2024},
  url={https://github.com/your-org/nfl},
  license={Mixed: GPL-3.0, CERN-OHL-S v2, CC BY-SA 4.0}
}
```

---

## 📄 License Summary

This project is licensed under multiple licenses depending on the component:
- **Firmware & Software**: GNU General Public License v3.0
- **Hardware**: CERN Open Hardware License v2 (Strongly Reciprocal)
- **Documentation**: Creative Commons Attribution-ShareAlike 4.0

See individual component directories for full license text.

---

**"Hearing is free and a right for everyone."**

Last Updated: 2024  
Status: Active Development
