
# RTrap — Ransomware Detection and Containment System (Python Research Prototype)

**RTrap** is a machine-learning-based deception system that traps ransomware by using intelligently generated decoy files and real-time monitoring to contain attacks. This project is a beginner-friendly Python implementation based on the IEEE paper [“RTrap: Trapping and Containing Ransomware With Machine Learning”](https://ieeexplore.ieee.org/document/10026355).

---

## 🔧 Prerequisites

- **Windows 10+ (recommended)** or Linux (optional)
- **Python 3.7+**
- **Admin privileges** to kill processes and disable network

### Install dependencies
```bash
git clone https://github.com/your-username/rtrap-prototype.git
cd rtrap-prototype
python -m venv venv
venv\Scripts\activate      # On Windows
pip install -r requirements.txt
```

---

## 📁 Project Structure

```bash
RTrap/
├── decoy_generator/
│   └── generator.py        # ML-based decoy file creator (uses Affinity Propagation)
├── decoy_watcher/
│   └── watcher.py          # Watches decoys for changes and contains ransomware
├── simulations/
│   └── fake_ransom.py      # Example ransomware script (safe for testing)
├── data/                   # Sample user files (txt, docx, etc.)
├── requirements.txt        # Python dependencies
└── README.md               # You are here
```

---

## 🧠 Component 1: Decoy Generator

### How it works
- Scans a target folder (`data/`)
- Extracts features from files: size, type, modified time, etc.
- Clusters them using **Affinity Propagation** (no need to set number of clusters!)
- Picks representative files as decoys
- Copies these as `*_decoy.*` files

### Run it
```bash
python decoy_generator/generator.py
```

---

## 🛡️ Component 2: Decoy Watcher

### How it works
- Monitors all decoy files in real time
- If a decoy is changed, it:
  - Kills the process that accessed it (using `psutil`)
  - Disables the network (Windows: `netsh`, Linux: `nmcli`)
  - Logs and stops further damage

### Run it
```bash
python decoy_watcher/watcher.py
```

---

## 💣 Ransomware Simulation (For Testing)

**⚠️ Use only on test files!**

### Simulated Attack
```bash
python simulations/fake_ransom.py
```
This script encrypts files in `data/` using a simple symmetric algorithm (`cryptography.fernet`). If a decoy is touched, the watcher will detect it and stop the attack.

---

## 🔗 Useful References

- [RTrap Research Paper (IEEE)](https://ieeexplore.ieee.org/document/10026355)
- [Affinity Propagation in scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AffinityPropagation.html)
- [Watchdog Docs (Python file monitoring)](https://python-watchdog.readthedocs.io/en/latest/)
- [psutil Docs (Process inspection)](https://psutil.readthedocs.io/en/latest/)
- [Educational Ransomware Simulator (GitHub)](https://github.com/atilsamancioglu/44-PythonRansom)
- [Ransomware-PoC (GitHub)](https://github.com/jimmy-ly00/Ransomware-PoC)

---

## 🧪 Future Enhancements
- UI dashboard (web or tkinter)
- Logging alerts to email/Slack
- Extend to detect fileless ransomware
- Deploy as Windows service or daemon

---

## 🧑‍💻 Author

Manvendra K Singh — *For learning & research purposes only*  
[LinkedIn]([https://www.linkedin.com/in/priyanshu-acharya-19164b255](https://www.linkedin.com/in/manvendrasingh07))

---

## 🛑 Disclaimer

This code is intended for **educational and research purposes** only. Do **NOT** use on real systems or deploy in production without proper evaluation.

