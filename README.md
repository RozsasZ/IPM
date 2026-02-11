# Intelligent Pedestrian Model (IPM)

The Intelligent Pedestrian Model (IPM) provides **risk‑based pedestrian prioritization** for ADAS and automated driving systems.  
Instead of treating all potential conflicts equally, IPM ranks pedestrians according to:

1. **Exposure** – likelihood of conflict (TTC, PET, contextual cues)  
2. **Severity** – epidemiologically grounded injury‑risk weighting based on impact speed

The model outputs a real‑time **risk score** and a **ranked list** of pedestrians for a given scene.

---

## 🚀 Key Features

### ✓ **Surrogate Safety Measures (SSM)**
- **Time-to-Collision (TTC)** and  
- **Post-Encroachment Time (PET)**  
are used to define conflict criticality. Both measures are widely validated and used for proactive safety assessment.  
[1](https://github.com/scikit-learn/scikit-learn/issues/32049) [2](https://deus-ex-machina-ism.com/?p=65217&lang=en)

### ✓ **Ranking Metric: NDCG@K**
IPM evaluates risk-ranking performance using **Normalized Discounted Cumulative Gain (NDCG)**:  
- emphasizes correctness at the **top of the list**  
- supports multi-level relevance  
- has strong theoretical backing in learning-to-rank literature[3](https://www.scirp.org/reference/referencespapers?referenceid=2384888) [4](https://www.docin.com/p-1721338439.html)

### ✓ **Severity Modeling (EU / US Profiles)**
IPM integrates epidemiological injury‑risk curves:
- **EU baseline (GIDAS / Tefft-type curves)** for injury risk vs. speed  
  [5](https://opentrafficcam.org/overview/usecases/trafficsafety/)
- **US IIHS curves** capturing higher SUV/pickup hood‑edge geometry, shifting risk curves leftwards  
  [6](https://www.computer.org/csdl/proceedings-article/iccv/2019/480300g261/1hVlQiCTlMA)

This Severity term makes IPM fundamentally different from typical intent or trajectory models.

---

## 📊 Supported Datasets

### **inD (EU, drone‑based, high‑precision trajectories)**
Ideal for TTC/PET ground truth and risk benchmarking.  
[7](https://www.jamiesnape.io/software/)

### **PIE (on‑board camera, intent labels, OBD data)**
Strong baseline for intent prediction; best published accuracy: **~79%**.  
[8](https://dblp.org/rec/conf/colt/WangWLHL13)

### **JAAD (context-rich pedestrian behavior dataset)**
Includes demographics, traffic-light states, behaviors, etc.  
citeturn2search15

---

## 📈 State-of-the-Art Comparison (High-Level)

| Model | Native Output | Can be Ranked? | Severity Included? | Reference |
|-------|---------------|----------------|---------------------|-----------|
| **IPM (this repo)** | Risk = Exposure × Severity | Yes | **Yes** | [5](https://opentrafficcam.org/overview/usecases/trafficsafety/)[6](https://www.computer.org/csdl/proceedings-article/iccv/2019/480300g261/1hVlQiCTlMA) |
| PIE Intent Model | Intent accuracy (~79%) | Yes (p_cross) | No | [8](https://dblp.org/rec/conf/colt/WangWLHL13) |
| Social‑LSTM | ADE/FDE | Yes (collision probability from sampled trajectories) | No | [9](https://books.google.com/books/about/Multiple_Criteria_Decision_Making.html?id=vTayAAAAIAAJ) |
| Trajectron++ | ADE/FDE | Yes | No | [10](https://davidakenny.net/kkc/c2/c2.htm) |
| Conflict‑DNN (Formosa et al.) | ~94% conflict classification accuracy | Yes (probability → score) | No | [11](https://scispace.com/papers/trajectron-dynamically-feasible-trajectory-forecasting-with-2tgshl9z2x) |
| LambdaMART | Ranking model (LTR) | Yes | Only if manually added | [12](https://github.com/StanfordASL/Trajectron-plus-plus) |

---

## 📚 Full Scientific Validation
See:  
**[`docs/VALIDATION.md`](docs/VALIDATION.md)**  
This includes visual explanations, ranking logic, and citations.

---

## 📄 License
MIT
