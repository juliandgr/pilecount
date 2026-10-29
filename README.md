# Acoustic Pile Driving & Foot-by-Foot Blow Counter
### DelDOT / AASHTO Compliant Infrastructure Pipeline

An automated, field-tested acoustic processing engine designed for DelDOT / AASHTO bridge and foundation pile inspection.

Runs in **two flexible modes**:
1. **Universal Client-Side Web Application (`index.html`)**: Deploy directly to **GitHub Pages** (or open locally). Works across **all devices** (iPhone Safari, Android Chrome, iPad, Windows, macOS) with zero server or Python required. Ingests live microphone streams (with device picker for AirPods/USB mics), processes uploaded `.m4a`/`.wav`/`.mp3` voice memos 100% client-side, and features an automated **Foot-by-Foot Lap Depth Tracker** to eliminate the paper clipboard bottleneck!
2. **Batch Processing Python Pipeline (`acoustic_pile_processor/`)**: Command-line interface and test harness for local workstation batch analysis and 4-panel diagnostic plot generation.

---

## 1. Deploying to GitHub Pages (All Devices & Phones)

Because the web application is built with 100% client-side Web Audio API and HTML5 Canvas, it requires **zero backend servers or Python installation on mobile phones**.

### Instant GitHub Pages Deployment:
1. Push this repository to GitHub.
2. In your GitHub repository, navigate to: **Settings &rarr; Pages**.
3. Under **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **`main`** (or `master`), Folder: **`/ (root)`**
   - Click **Save**.
4. GitHub Pages will generate your public live URL (e.g. `https://<your-username>.github.io/<repository-name>/`).
5. Open this URL in **Safari on your iPhone**, **Chrome on Android**, or any device!

---

## 2. Key Web App Capabilities (`index.html`)

- **100% English Codebase & UI**: All variables, identifiers, comments, labels, and export keys adhere to English engineering standards.
- **Audio File Upload Ingestion**: Drag-and-drop or upload iPhone voice memos (`.m4a`, `.wav`, `.mp3`). Audio is decoded and analyzed client-side via `AudioContext.decodeAudioData()`.
- **Live Mobile Microphone Streaming**: Direct microphone access (`getUserMedia`) with an **Audio Input Device Selector** (Built-in mic, Bluetooth AirPods, USB headsets).
- **Automated Foot-by-Foot Depth Tracking ("Next Foot / Lap" System)**:
  - Inspector sets initial depth (e.g. `16 ft`).
  - Screen displays **Current Foot Blows** and **Cumulative Total Blows**.
  - A giant tap button: **`[ RECORD FOOT & NEXT (16' -> 17') ]`** (also triggered via Spacebar or Enter).
  - Tapping saves the foot interval, advances target depth to `17 ft`, resets the current foot counter to zero without stopping the total count, and plays a dual-tone earbud chime (`C5 -> E5`) so the inspector never has to look away from the pile markings!
- **DelDOT Standard Specification 605.3.8 Real-Time Compliance**:
  - Live alerts if driving resistance exceeds **120 blows per foot**.
  - Live alerts if practical refusal threshold is reached (**>= 20 blows per inch**).
- **Live 60 FPS Oscilloscope**: Real-time canvas rendering of filtered audio waveforms, rolling adaptive threshold lines, and red strike marker pins.
- **One-Click Export**: Export DelDOT IDR logs as CSV (Excel), DelDOT JSON, or formatted clipboard text.

---

## 3. Local Mobile Testing Server (`serve_mobile.py`)

If testing on your local Wi-Fi network before pushing to GitHub:

```powershell
# Start local server with automatic HTTPS support for iOS Safari
python serve_mobile.py --ssl
```

- Open on desktop: `https://localhost:8000/`
- Open on iPhone: `https://<YOUR_LOCAL_IP>:8000/`

---

## 4. Workstation Python Pipeline & Test Harness

```powershell
# 1. Activate Python virtual environment
.\.venv\Scripts\activate

# 2. Run automated unit test suite (100% pass)
python -m unittest acoustic_pile_processor.test_harness -v

# 3. Run synthetic self-test with diagnostic plot generation
python run_pipeline.py --test

# 4. Batch process field recordings
python run_pipeline.py path/to/field_memo.m4a --hammer diesel_pile_hammer --depth 12.0
```

---

## 5. File Manifest

```
quirky-archimedes/
├── index.html                # Universal GitHub Pages web app (100% English)
├── realtime_pile_counter.html # Mirror copy of index.html
├── serve_mobile.py           # Local mobile server with SSL
├── run_pipeline.py           # Top-level Python CLI runner
├── requirements.txt          # Python dependencies
├── README.md                 # Project documentation
└── acoustic_pile_processor/  # Python batch processing engine
    ├── __init__.py
    ├── config.py
    ├── audio_loader.py
    ├── preprocessor.py
    ├── blow_counter.py
    ├── deldot_reporter.py
    ├── visualizer.py
    ├── web_visualizer.py
    ├── synthetic_audio.py
    ├── pipeline.py
    ├── cli.py
    └── test_harness.py
```

---

## Author Attribution & Legal Framework

### Principal System Architect & Creator
- **Author & Developer:** **Julian Gomez-Rodriguez** (`jgome` / Julian Gomez)
- **Role:** Heavy Highway & Civil Infrastructure Field Inspector / Daily Work Report (IDR) Specialist
- **Context:** DelDOT Highway & Bridge Infrastructure Projects (e.g., SR-54 Lighthouse Rd, BR3-437)
- **Application:** `PILECOUNT.` Acoustic Pile Driving & Pile Cap Blow Count Audio Processor

### Legal Framework, Non-Endorsement Notice & Terms of Use
1. **Independent Field Calculation Tool:** `PILECOUNT.` is an independent engineering calculation and mobile field assistance utility created by Julian Gomez-Rodriguez for field research, transient acoustic analysis, and inspection efficiency.
2. **Non-Endorsement & Affiliation Disclaimer:** This software is **NOT** affiliated with, sponsored by, authorized by, or endorsed by the Delaware Department of Transportation (DelDOT), the American Association of State Highway and Transportation Officials (AASHTO), the Federal Highway Administration (FHWA), or any governmental department, public agency, or municipality. References to *DelDOT Standard Specifications Section 605* or *AASHTO LRFD Construction Specifications* are for computational benchmark reference and field alignment only.
3. **Internal Test Build & Testing Purpose:** Deployed strictly as an **Internal Test Build** for experimental field testing, calculation aid, and acoustic evaluation. It is not certified as an automated legal instrument of record.
4. **Professional Judgment & Inspector of Record Responsibility:** Automated blow counts, cadence (BPM) estimations, and foot-by-foot driving logs are mathematical approximations derived from acoustic digital signal processing (DSP). Certified Field Inspectors and Engineers of Record retain sole and ultimate responsibility for manually monitoring physical pile depth markings, hammer drop heights, penetration per blow, practical refusal criteria, and the submission of official inspection logs (IDR / DWR).
5. **Limitation of Liability & "AS IS" Disclaimer:** Provided "AS IS" and "WITH ALL FAULTS," without warranty of any kind, express or implied. Under no circumstances shall the author or contributors be liable for construction claims, delays, structural damage, foundation misinterpretations, or damages arising out of the use or reliance upon this software.
6. **AI-Assisted Development Notice:** This software and DSP pipeline were developed with the assistance of Artificial Intelligence (AI). Human engineering oversight and physical field verification are required prior to utilizing data for official IDR/DWR records.
