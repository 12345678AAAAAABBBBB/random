# RTrap: Ransomware Trapping and Containment System (Python Research Prototype)

This is a beginner-friendly research prototype implementation of **RTrap** — a machine learning-based system that detects and contains ransomware attacks by planting adaptive decoy files and monitoring them in real time.

---

## 🛠 Prerequisites

Before you begin, make sure you have the following:

- **Windows OS** (preferred) or Linux.
- **Python 3.7+** installed.
- Administrator privileges for containment actions like network disable or process kill.
- Basic knowledge of Python and file systems (recommended but not required).

---

## 📁 Project Folder Structure

```
RTrap/
├── decoy_generator/
│   └── generator.py         # Decoy file creator using Affinity Propagation
├── decoy_watcher/
│   └── watcher.py           # Real-time monitoring and containment
├── simulations/
│   └── ransomware_sim.py    # Controlled ransomware simulation
├── data/                    # Folder with test user files
├── requirements.txt
└── README.md
```

---

## 🔧 Step 1: Setup the Environment

```bash
# Create virtual environment
python -m venv rtrap-env
rtrap-env\Scripts\activate    # On Windows

# Install dependencies
pip install -r requirements.txt
```

**requirements.txt**
```
scikit-learn
watchdog
psutil
cryptography
```

---

## 🧠 Step 2: Generate Adaptive Decoy Files

1. Place some sample documents in the `data/` folder (e.g., `.txt`, `.pdf`, `.docx`).

2. Run the decoy generator:
```bash
python decoy_generator/generator.py
```

- Uses Affinity Propagation from `scikit-learn`.
- Picks representative user files and creates decoy versions (`*_backup.*`).

---

## 🛡️ Step 3: Start the Decoy-Watcher (Live Monitoring)

```bash
python decoy_watcher/watcher.py
```

- Monitors all decoy files for any changes.
- On access/modification, it:
  - **Identifies the attacking process**
  - **Kills it using `psutil`**
  - **Disconnects internet/network**
  - Logs the attack and optionally notifies (can be extended).

---

## 🧪 Step 4: Simulate a Ransomware Attack

> ⚠️ **Do not run real ransomware. Use simulation only.**

Run the educational ransomware simulator to test detection:

```bash
python simulations/ransomware_sim.py
```

- Encrypts files in `data/` folder.
- If a decoy is touched, RTrap immediately triggers containment.

---

## 💡 GitHub Projects to Study

Here are safe and useful repositories to learn from or extend:

- 🔗 [watchdog (file monitoring lib)](https://github.com/gorakhargosh/watchdog)
- 🔗 [PythonRansom (simple ransomware PoC)](https://github.com/atilsamancioglu/44-PythonRansom)
- 🔗 [ransomware-poc (AES encryption)](https://github.com/jimmy-ly00/ransomware-poc)
- 🔗 [Affinity Propagation in sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AffinityPropagation.html)

---

## 🧩 Future Improvements

- GUI for decoy status.
- Cloud logging / alerting.
- Linux support script.
- Process forensics (hashing, logging, etc).
- Automatic decoy regeneration over time.

---

## 📖 Reference

This project is based on the IEEE research paper:

> Ganfure et al., *"RTrap: Trapping and Containing Ransomware With Machine Learning,"* IEEE Transactions on Information Forensics and Security, 2023.

[Download paper from IEEE Xplore](https://ieeexplore.ieee.org/document/10032560)  
DOI: [10.1109/TIFS.2023.3240025](https://doi.org/10.1109/TIFS.2023.3240025)

---

## ✅ Credits

Created for learning and demonstration purposes. Not intended for production or real-world ransomware combat. For ethical and academic use only.

---
