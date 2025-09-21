# nova — GNN Track Reconstruction & Anomaly Trigger  
**Upcoming · personal project**

**One line:** Graph-aware track reconstruction on CMS Open Data, plus a reproducible low-latency trigger prototype (ONNX → edge GPIO).

---

## Snapshot
A compact, no-fluff repo to experiment with: convert detector hits into graphs, train/validate a GNN that groups hits into charged-particle tracks, add a lightweight anomaly signal, and measure end-to-end inference latency on an edge device. Clean notebooks, reproducible sample data, and a short demo are the deliverables.

---

## Core idea (very short)
Use message-passing over hit-graphs to replace/augment combinatorial tracking; export a runnable model for low-latency inference and trigger emulation.

---

## Quick specs
- Input: per-event hits (x,y,z,layer,time,energy) from CERN Open Data (small derived sample)  
- Model: PyTorch / PyG message-passing GNN (edge-classification → connected-components → tracks)  
- Anomaly: track-level autoencoder / simple scoring head  
- Export: ONNX + runtime profiling (desktop + Raspberry Pi)  
- Metrics: tracking efficiency, fake rate, ROC/AUC, inference latency (ms)

---

## Progress tracker
- [x] Project skeleton & README  
- [ ] Sample dataset + ingestion (ROOT → npz/parquet)  
- [ ] Graph builder (kNN / layer adjacency)  
- [ ] Baseline greedy tracker & metrics  
- [ ] GNN prototype (train/eval)  
- [ ] Anomaly head & tests  
- [ ] ONNX export + quantization experiments  
- [ ] Raspberry Pi trigger demo + GPIO verification  
- [ ] Docker image, notebook walkthrough, demo video

---

## Minimal dev quickstart
> Intended for the early-stage dev snapshot (small sample included).

```bash
# clone
git clone https://github.com/<you>/nova.git
cd nova

# create env
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# run a tiny reproducible demo (uses packaged sample data)
python src/ingest_demo.py         # converts ROOT→npz (sample)
python src/build_graphs.py        # build a few graphs and save
python src/train_toy.py --epochs 3
python src/eval_toy.py
