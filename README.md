# ✈️ AeroAssist: Multimodal AI for Aircraft Maintenance

> **Published at:** IEEE Aerospace Conference 2026
> **Best Paper Award:** IEEE/AIAA DASC 2025

## 💡 The Problem

A slight visual crack on a turbine blade might mean nothing on its own. But combine it with an unusual vibration pattern in the audio AND a slow pressure drift in the sensor data — now you have a strong signal for metal fatigue. Traditional systems analyze each data type in isolation and miss these correlations. By the time the problem is caught, it's an unscheduled shutdown costing millions.

## 🚀 The Solution

AeroAssist is a **prompt-driven multimodal diagnostic framework** built on **Google Gemini 2.5 Pro** — no fine-tuning, no retraining, no expensive labeled datasets. It processes video, audio, and sensor data in a **single inference call** and reasons across all three modalities like a human expert would.

The secret sauce is **Guided Reflective Diagnostic Reasoning (RDR)** — a 4-phase structured prompting strategy we designed:

### Phase 1: Independent Analysis
> "Looking at ONLY the video, what do you observe?"
> "ONLY the audio — anything unusual?"
> "ONLY the sensor data — any anomalies?"

Each modality analyzed in isolation. No bias from one channel contaminating another.

### Phase 2: Cross-Modal Synthesis & Self-Critique
> "Now consider all three together. Do the anomalies correlate? Does the crack location match where the vibration spike occurs?"

This is where multimodal power shows up — correlations invisible in any single stream become obvious.

### Phase 3: Formalized Diagnostic Report
Structured JSON output with classification (Good / Not Bad / Bad), severity assessment, and recommended action.

### Phase 4: Executive Summary
Human-readable summary with the final diagnosis, main finding, and primary recommendation.

---

## 📊 Key Results

| Setting | Accuracy |
|---------|----------|
| Zero-shot (no examples) | Strong baseline performance |
| Few-shot (with examples) | **90% classification accuracy** |

The few-shot approach uses ~80,000 tokens of context with complete example reasoning chains — teaching the model not just the output format but the depth and style of expert-level diagnostic thinking.

---

## 🧠 Why No Fine-Tuning?

Aerospace fault data is extremely scarce. A specific turbine fault might have 5-10 documented cases worldwide. Fine-tuning on 5 examples = instant overfitting. Gemini 2.5 Pro already understands what cracks look like, what mechanical sounds mean, and what sensor anomalies indicate from pre-training. RDR structures HOW it applies that knowledge.

---

## 🔍 Interesting Failure Modes

The framework isn't perfect — and we documented that honestly:
- **Attentional blindness** — the model occasionally overlooks obvious visual defects when sensor data looks normal, showing over-reliance on one modality
- **Contradictory evidence** — when modalities disagree, the model can resolve conflicts but sometimes defaults to the "safer" diagnosis

These findings position AeroAssist as a diagnostic **co-pilot**, not an autonomous agent. Human oversight remains essential.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Foundation Model | Google Gemini 2.5 Pro / Flash |
| Input Modalities | Video + Audio + Sensor Data |
| Prompting Strategy | Guided Reflective Diagnostic Reasoning (RDR) |
| Evaluation | Semi-synthetic aerospace dataset, 30 test cases |
| Output | Structured JSON diagnostic reports |

---

## 📁 Repo Structure
├── main.py.py          # Main pipeline — video + audio + sensor processing through Gemini
├── Prompt data/        # RDR prompt templates — all 4 phases with few-shot examples
├── test_data/          # Semi-synthetic aerospace test cases
└── Results.xlsx        # Evaluation results and analysis

---

## 📄 Citation
S. Kalari, A. Panchumarthi, V. Ashok, R. Mukkamala.
"AeroAssist: A Prompt-Driven Multimodal AI Framework for Aircraft Maintenance."
IEEE Aerospace Conference, 2026.
