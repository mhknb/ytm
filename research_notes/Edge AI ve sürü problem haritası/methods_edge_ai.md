# Emerging Methodological Approaches in Low-Power / Edge AI and TinyML (2024-2026): Maturity, Open Gaps, Edge Portability, Defense Coverage

Scope note for the report writer: these notes are about methods only. No thesis topics are proposed. Sources come in three tiers. (a) Items found or confirmed by web search in this session. (b) Well-known anchor papers recalled from prior knowledge, marked "(not re-verified this session)". (c) arXiv preprints, flagged as such. Direct fetches of arxiv.org failed during this session (DNS error), so arXiv details come from search-engine snippets/abstracts, not full-text reads. Scimago quartiles are marked "unverified" unless stated. Maturity scale used below: **L1** = lab/preprint only; **L2** = peer-reviewed method + MCU/edge demo; **L3** = benchmarked across devices / open toolchain support; **L4** = vendor/production toolchain support.

---

## 1. On-device training, continual learning and few-shot class addition on MCUs / edge devices

### Takeaway
On-device learning on MCUs is technically feasible: sparse/partial backprop runs in <256 KB SRAM, and TTA is feasible in 512 KB. But it is still L2 maturity. A 2026 survey of 70 TinyML on-device-learning works finds that application-oriented work in the concept-drift and continual-learning regimes is "almost entirely absent". It also finds that methodological work clusters on image-classification benchmarks too heavy for real TinyML deployments. Defense uses (drone detection, GNSS interference, RF/acoustic nodes) appear essentially unexplored for *on-device* learning.

### Cited Findings
- **Survey (2026, preprint):** "What changes after deployment? A survey on On-device Learning in TinyML" (arXiv 2605.31226). It reviews 70 on-device learning solutions organized by distribution-change regime. Application-oriented works in the concept-drift and continual-learning regimes "remain almost entirely absent", which the authors attribute to (i) the difficulty of obtaining labels in non-stationary settings and (ii) the lack of realistic benchmarks. Methodological works cluster around image-classification benchmarks "too demanding for most real-world TinyML deployments". On hardware, the heaviest computation consistently sits in the *frozen feature-extractor inference pass*, not in the update. — [arXiv 2605.31226](https://arxiv.org/pdf/2605.31226) (authors/venue not verified this session; preprint, quartile n/a)
- **Survey (2024 arXiv version of a 2023 magazine paper):** Lin, Zhu, Chen, Wang, Gan, Han (MIT), "Tiny Machine Learning: Progress and Futures". It covers tiny on-device training, motivated by privacy and by fine-tuning on-device instead of sending data to the cloud. It names self-supervised tasks designed for on-device training as an emerging direction for the missing-label problem. — [arXiv 2403.19076](https://arxiv.org/abs/2403.19076); published in IEEE Circuits and Systems Magazine 2023, DOI 10.1109/MCAS.2023.3302182 (venue/DOI not re-verified this session; quartile unverified)
- **Survey (2025, preprint):** "From Tiny Machine Learning to Tiny Deep Learning: A Survey". It covers continual learning on MCUs and cites TinyOL as a framework for online learning on MCUs. It also catalogs deployment frameworks, compilers and AutoML tools for on-device learning. — [arXiv 2506.18927](https://arxiv.org/abs/2506.18927)
- **Survey (2025, preprint):** a survey of deep learners at the edge names catastrophic forgetting, data inefficiency, and handling IoT tabular data in open-world settings as key open challenges. — [arXiv 2502.17788](https://arxiv.org/abs/2502.17788v1)
- **Older review (2022):** all on-device training frameworks at the time worked only with networks having "simple and limited architectural choices" to prevent resource overflow. — [arXiv 2205.14550](https://arxiv.org/pdf/2205.14550)
- **Anchor methods (not re-verified this session):**
  - Lin et al., "On-Device Training Under 256KB Memory" (NeurIPS 2022). Quantization-aware scaling plus sparse update plus the Tiny Training Engine. The first full CNN fine-tuning on an MCU. — [arXiv 2206.15472](https://arxiv.org/abs/2206.15472)
  - Kwon et al., "TinyTrain: Resource-aware task-adaptive sparse training of DNNs at the data-scarce edge" (ICML 2024). Few-shot, task-adaptive sparse update on MCUs. — [arXiv 2307.09988](https://arxiv.org/abs/2307.09988)
  - Zhu et al., "PockEngine: Sparse and Efficient Fine-tuning in a Pocket" (MICRO 2023). Compile-time sparse backprop graph for edge devices including Jetson. — [arXiv 2310.17752](https://arxiv.org/abs/2310.17752)

### Inferences
- **Maturity:** L2 for MCU fine-tuning and few-shot head/bias updates. L1 for true class-incremental continual learning on MCUs, because replay buffers, forgetting control and label acquisition on-node are unresolved.
- **Methodological gaps (from surveys):**
  - label scarcity in non-stationary streams;
  - no realistic drift/CL benchmarks for MCU-class tasks (audio, IMU, RF), only scaled-down image benchmarks;
  - the inference pass of the frozen backbone dominates cost, so "cheap update" methods do not address the real energy bottleneck;
  - integer-only runtimes (TFLM, CMSIS-NN) do not natively store activations or optimizer state (see FORGE in §5).
- **Portability:**
  - MCU (STM32H7, nRF, Cortex-M7) is demonstrated, but via research engines (TTE, TinyOL), not vendor toolchains. STM32Cube.AI, TFLM, Hailo and TensorRT are inference-oriented.
  - Jetson supports PyTorch-level fine-tuning natively.
  - Hailo/Akida-style NPUs: inference only. The exception is Akida's last-layer few-shot "edge learning" (not verified this session).
- **Defense coverage:** I found no 2024-2026 paper applying on-device continual or few-shot class addition to drone/FPV detection, GNSS interference detection or RF sensing nodes. A new drone type, a new jammer waveform or a new acoustic signature are natural "new class after deployment" cases that the surveys say are missing from application-oriented work.

### Gaps
- Could not fetch the full text of arXiv 2605.31226 to extract author names and the full open-challenges list.
- No verified source on whether STM32Cube.AI / X-CUBE-AI or TFLM officially support on-device training as of 2026.

---

## 2. Quantization (sub-8-bit, mixed precision), pruning, hardware-aware NAS, compiler/deployment toolchains

### Takeaway
INT8 post-training quantization plus TFLM / STM32Cube.AI / TensorRT / Hailo Dataflow Compiler is production-grade (L4). Sub-8-bit and mixed-precision quantization on MCUs, and hardware-aware NAS, are L2-L3. Their main gaps: weak kernel/ISA support for sub-byte arithmetic on commodity MCUs, missing cross-toolchain reproducibility, and too few surveys that treat optimization and hardware jointly.

### Cited Findings
- **Survey (2025, preprint, revised to v4 in Jan 2026):** Abushahla et al., "Neural Network Quantization for Microcontrollers: A Comprehensive Survey of Methods, Platforms, and Applications". Takes a hardware-first view. It covers trade-offs between model performance and MCU memory hierarchies, numerical representations and accelerator support, and evaluates software frameworks and hardware platforms for quantized networks on MCUs. It notes that hardware-focused surveys tend to *omit* model-optimization strategies. — [arXiv 2508.15008](https://arxiv.org/abs/2508.15008v4)
- **Survey (2025, preprint):** "From TinyML to TinyDL" analyzes quantization, pruning and NAS. It tracks hardware trends from MCUs to dedicated neural accelerators and catalogs compilers and deployment frameworks. — [arXiv 2506.18927](https://arxiv.org/abs/2506.18927v2)
- **Quantization latency caveat:** a 2026 TU Delft thesis on Mamba-on-MCU (TFLM) found that quantization substantially reduces memory but can add *latency overhead* on hardware that lacks INT8 acceleration. — [TU Delft repository](https://repository.tudelft.nl/record/uuid:1d2c2f73-f702-4d94-9af3-1dca52275665) (bachelor thesis; low evidence tier)
- **Benchmark anchor (not re-verified this session):** Banbury et al., "MLPerf Tiny Benchmark" (NeurIPS Datasets & Benchmarks 2021). Four tasks: keyword spotting, visual wake words, image classification, anomaly detection. Latency/energy measured on MCUs. — [arXiv 2106.07597](https://arxiv.org/abs/2106.07597)
- **HW-aware NAS anchors (not re-verified this session):**
  - Lin et al., MCUNet (NeurIPS 2020): TinyNAS plus the TinyEngine co-design. — [arXiv 2007.10319](https://arxiv.org/abs/2007.10319)
  - MCUNetV2 (NeurIPS 2021): patch-based inference for detection on MCUs. — [arXiv 2110.15352](https://arxiv.org/abs/2110.15352)
  - Benmeziane et al., "A Comprehensive Survey on Hardware-Aware Neural Architecture Search". — [arXiv 2101.09336](https://arxiv.org/abs/2101.09336)
- **Mixed-precision on MCUs anchor (not re-verified this session):** Rusci, Capotondi, Benini, "Memory-Driven Mixed Low Precision Quantization for Enabling Deep Network Inference on Microcontrollers" (MLSys 2020). — [arXiv 1905.13082](https://arxiv.org/abs/1905.13082)
- **GNSS-specific compression example:**
  - Dictionary-based contrastive learning for GNSS jamming detection uses transfer learning plus contrastive embeddings, combined with pruning and distillation, to shrink the classifier for embedded hardware. The authors claim real-time feasibility at the edge. — [arXiv 2512.07512](https://arxiv.org/abs/2512.07512) (preprint)
  - Wegner et al. (2026) use 8-bit-quantized VAEs on a Google Edge TPU to compress raw GNSS data (>42x) and classify jamming/spoofing. F2 = 0.915 on reconstructed vs 0.923 on original signals. — [arXiv 2605.14839](https://arxiv.org/abs/2605.14839) (preprint)

### Inferences
- **Maturity:**
  - INT8 PTQ/QAT: L4.
  - Unstructured pruning on MCUs: L2 at best. Commodity MCU kernels rarely exploit sparsity, so only structured/channel pruning reliably converts into latency.
  - Sub-4-bit / mixed precision on MCUs: L2 (research kernels).
  - HW-aware NAS: L3 (MCUNet, Micronets), but expensive and tied to specific latency models.
- **Methodological gaps:**
  - sub-byte kernels are missing in mainstream runtimes;
  - accuracy-latency-energy predictors do not transfer across toolchains (TFLM vs STM32Cube.AI vs TVM);
  - NAS search spaces rarely include non-CNN operators (SSMs, attention, spiking);
  - most evaluations use MLPerf-Tiny-like vision/audio tasks, rarely RF/IQ or GNSS signal inputs;
  - few joint quantization + robustness studies (quantization effects on calibration and OOD behavior; see §5).
- **Portability:**
  - **MCU:** TFLM, STM32Cube.AI, CMSIS-NN, TVM/microTVM, all INT8-centric.
  - **NPU:** Hailo (Dataflow Compiler; INT8/INT4 weights) and Edge TPU (INT8 only) constrain the operator set.
  - **Jetson:** TensorRT supports FP16/INT8, plus FP8/INT4 on newer Orin/Thor-class parts. Exact supported precisions per device not verified this session.
- **Defense coverage:**
  - Applied: GNSS jamming classifiers (above), acoustic drone detectors on STM32 (see §7), and YOLO-family drone detectors on Jetson (widely reported, not individually verified here).
  - Not found: sub-4-bit / mixed-precision or HW-NAS studies specifically targeting RF-based drone detection or GNSS interference on MCUs.

### Gaps
- No verified Scimago quartile for any of the above. The surveys are arXiv preprints whose journal publication status was not confirmed.
- No 2024-2026 head-to-head benchmark of TFLM vs STM32Cube.AI vs TVM vs Hailo vs TensorRT was found in this session.

---

## 3. Spiking neural networks, neuromorphic hardware (Loihi 2, Akida, SynSense) and event cameras

### Takeaway
Neuromorphic sensing and compute are moving from L1 to L2 for defense-relevant sensing. A 2025 FOI (Sweden) preprint shows an event-camera + SNN + neuromorphic-chip drone "virtual tripwire" that is orders of magnitude more energy-efficient than an edge-GPU baseline. Field-level reviews (Nature 2025) still name scale, software ecosystem and benchmarking as the main barriers. Standardized benchmarking (NeuroBench) has only just appeared.

### Cited Findings
- **Review (Nature, 2025):** Kudithipudi et al. (23 authors), "Neuromorphic computing at scale", Nature 637, 801-812, DOI 10.1038/s41586-024-08253-8. It argues the field is at a "critical juncture", with scale as a key progress metric. Systems must grow considerably to tackle complex real-world problems, and a broader ecosystem is needed. Cites Intel Hala Point (1.15 billion neurons). — [ORNL record](https://impact.ornl.gov/en/publications/neuromorphic-computing-at-scale/); [UTSA news](https://www.utsa.edu/today/2025/01/story/nature-article-neuromorphic-computing-systems.html) (Nature: Scimago Q1, generally known; not checked on Scimago this session)
- **Earlier Loihi survey:** Davies et al., Proc. IEEE 2021. Brain-inspired networks that use recurrence, precise spike timing, plasticity, stochasticity and sparsity reach much lower latency and energy than conventional approaches, while *standard feedforward networks show little benefit*. — [Proc. IEEE page](https://proceedingsoftheieee.ieee.org/advancing-neuromorphic-computing-with-loihi-a-survey-of-results-and-outlook/)
- **Defense application, drone detection (2025, preprint):** "Drone Detection Using a Low-Power Neuromorphic Virtual Tripwire" (FOI Sweden).
  - Pipeline: event camera + SNN + neuromorphic chip. Multiple units form a virtual tripwire that detects when and where drones enter a restricted zone.
  - Energy: "several orders of magnitude more energy efficient" than an edge-GPU reference.
  - Explainability check: the model most likely relies on drone *shape* rather than the temporal signature of the propellers.
  - [arXiv 2509.12997](https://arxiv.org/abs/2509.12997v1)
- **Survey (Aug 2025, preprint):** an event-camera drone-detection survey from the Universities of Florence and Siena. It covers detection, tracking, trajectory forecasting and drone identification via propeller signatures, and promotes neuromorphic computing for counter-UAV. — [alphaXiv 2508.04564](https://alphaxiv.org/overview/2508.04564v1)
- **Hardware ecosystem for drones:** the SDU (Denmark) neuromorphic group lists BrainChip Akida, SynSense Speck and Innatera Pulsar as lightweight neuromorphic processors for drones, paired with event sensors such as Prophesee GenX320. — [SDU page](https://www.sdu.dk/en/forskning/sdu-digital-and-high-frequency-electronics/forskningsomraader/neuromorphic-computing)
- **Older precursors:**
  - STDP-trained deep convolutional SNN for UAV detection with a neuromorphic retina (ICANN 2019). The reported detection rate for other objects differs between versions (91% vs 92%). — [arXiv 1904.12230](https://arxiv.org/abs/1904.12230)
  - Event-based vision algorithm implemented as an SNN on a neuromorphic chip for drone *control*, with on-chip learning for online adaptation. — [arXiv 2108.03694](https://arxiv.org/pdf/2108.03694v1)
- **Event-vision anchor survey (not re-verified this session):** Gallego et al., "Event-based Vision: A Survey", IEEE TPAMI 44(1), 2022, DOI 10.1109/TPAMI.2020.3008413. — [arXiv 1904.08405](https://arxiv.org/abs/1904.08405) (TPAMI: Q1, generally known)
- **Benchmarking anchors (not re-verified this session):**
  - Yik et al., "The NeuroBench framework for benchmarking neuromorphic computing algorithms and systems", Nature Communications 2025. — [arXiv 2304.04640](https://arxiv.org/abs/2304.04640)
  - Shrestha et al., "Efficient Video and Audio Processing with Loihi 2" (ICASSP 2024). — [arXiv 2310.03251](https://arxiv.org/abs/2310.03251)

### Inferences
- **Maturity:**
  - Event cameras: L3-L4 as sensors (Prophesee, iniVation are commercial).
  - SNN training via surrogate gradients: L3 in software (snnTorch, Lava, Rockpool, Sinabs; library names not re-verified).
  - Deployment on Loihi 2: L2. Research-access only (Intel INRC).
  - Akida: L3. Commercial dev kits, CNN-to-SNN conversion.
  - SynSense Speck/Xylo: L2-L3. Low-power vision and audio SoCs.
- **Methodological gaps (Nature 2025 review, Proc. IEEE 2021, NeuroBench motivation):**
  - feedforward SNNs show little benefit over ANNs, so gains require exploiting temporal/sparse structure;
  - no standard cross-platform benchmarks (only now NeuroBench);
  - SNN-ANN accuracy gap on complex detection;
  - immature toolchains and conversion pipelines;
  - few fair energy comparisons with the same task, same accuracy and system-level power (sensor + chip + I/O);
  - explainability of what SNNs latch onto (the FOI paper's shape-vs-propeller finding shows this matters).
- **Portability:** not portable to MCU/Hailo/TensorRT as native SNNs. Event data *can* be framed (event histograms/voxel grids) and run as ANNs on Jetson or Hailo, which is a common baseline. Neuromorphic chips each need their own SDK (Lava for Loihi 2, MetaTF for Akida, SynSense SDKs).
- **Defense coverage:**
  - Applied: drone detection and tripwires (FOI 2025), counter-UAV event-vision (survey 2025), drone control (2021).
  - Not found: SNN/neuromorphic for GNSS interference detection, RF spectrum sensing on neuromorphic chips, or event-camera visual navigation in GNSS-denied settings evaluated on neuromorphic hardware. Event-based VIO exists in robotics literature, but on-chip neuromorphic deployment was not found.

### Gaps
- No 2024-2026 head-to-head of Loihi 2 vs Akida vs SynSense on the same drone-detection task was found.
- NeuroBench publication details (Nature Communications 2025, DOI) were not re-verified this session.

---

## 4. State-space models (Mamba), efficient transformers, tiny foundation models, and distillation from foundation models (DINOv2, CLIP, SAM) to tiny models

### Takeaway
Mamba/SSMs on MCUs are early (L1-L2). Inference demos exist for keyword spotting in ~60 KB RAM. A 2026 analysis argues that newer Mamba versions have *lost* edge efficiency. Foundation-model-to-edge distillation (DINOv2 → MobileNet/ViT-S, CLIP → EfficientNet, SAM → MobileSAM/EfficientSAM) is L3 on Jetson-class devices. Distilling to MCUs is L1 (single-author preprints).

### Cited Findings
- **MambaLite-Micro (2025, preprint):** memory-optimized Mamba inference on MCUs. Deploying sequence models on MCUs remains challenging due to memory, compute and power limits. — [arXiv 2509.05488](https://arxiv.org/abs/2509.05488)
- **TU Delft thesis (2026):** "Adapting Mamba Models for Deployment on Microcontrollers". A quantized Mamba in TFLM reaches 60.4 KB peak RAM on keyword spotting, reported as 74% less than MambaLite-Micro. Quantization can add latency on hardware without INT8 acceleration. Concludes Mamba is viable for TinyML but needs further optimization. — [TU Delft repository](https://repository.tudelft.nl/record/uuid:1d2c2f73-f702-4d94-9af3-1dca52275665) (bachelor thesis)
- **"The Hyperscale Lottery: How State-Space Models Have Sacrificed Edge Efficiency" (2026, preprint):** in the edge prefill regime (batch = 1), throughput *decreases* from Mamba-1 to Mamba-3. Later versions were tuned for cloud throughput. — [arXiv 2604.07935](https://arxiv.org/abs/2604.07935)
- **eMamba (Aug 2025, preprint):** an end-to-end hardware acceleration framework for Mamba on edge FPGA/ASIC. — [papers.cool 2508.10370](https://papers.cool/arxiv/2508.10370)
- **EdgeNavMamba (2025, preprint):** Mamba-based object detector plus knowledge distillation for navigation, validated on Jetson Orin Nano (8 GB) and Raspberry Pi 5. — [arXiv 2510.14946](https://arxiv.org/html/2510.14946v1)
- **Foundation-model distillation to edge:**
  - DINOv2-L teacher distilled into MobileNetV4, ViT-S and EfficientNet-B0, deployed with TensorRT (raptor classification, 2026 preprint). — [arXiv 2607.26238](https://arxiv.org/abs/2607.26238)
  - DINOv2 ViT-S/14 teacher → MobileViT student via embedding-MSE, for few-shot edge AI (2026 preprint). — [arXiv 2603.26145](https://arxiv.org/abs/2603.26145)
  - Clip4Retrofit: CLIP → EfficientNet-B3 + MLP projection heads that preserve cross-modal alignment, for in-vehicle cameras (2025 preprint). — [arXiv 2505.18039](https://arxiv.org/html/2505.18039v1)
  - TinyVLM: zero-shot detection in <1 MB via distilled vision-language Matryoshka embeddings, 26 FPS on STM32H7. Single-author independent preprint, so treat with caution. — [arXiv 2603.00136](https://arxiv.org/abs/2603.00136)
- **Anchors (not re-verified this session):**
  - Gu & Dao, Mamba (2023). — [arXiv 2312.00752](https://arxiv.org/abs/2312.00752)
  - MobileSAM. — [arXiv 2306.14289](https://arxiv.org/abs/2306.14289)
  - EfficientSAM (CVPR 2024). — [arXiv 2312.00863](https://arxiv.org/abs/2312.00863)
  - EfficientViT-SAM. — [arXiv 2402.05008](https://arxiv.org/abs/2402.05008)
  - MobileCLIP (CVPR 2024). — [arXiv 2311.17049](https://arxiv.org/abs/2311.17049)
  - TinyCLIP (ICCV 2023). — [arXiv 2309.12314](https://arxiv.org/abs/2309.12314)
  - AM-RADIO multi-teacher (DINOv2 + CLIP + SAM) agglomerative distillation (CVPR 2024). — [arXiv 2312.06709](https://arxiv.org/abs/2312.06709)

### Inferences
- **Maturity:**
  - SSMs on MCU: L1-L2.
  - SSMs on Jetson: L2.
  - FM→CNN/ViT-S distillation for Jetson/Hailo: L3 (many working pipelines).
  - FM→MCU (<1 MB) distillation: L1.
- **Methodological gaps:**
  - SSM selective-scan operators are not native in TFLM, STM32Cube.AI, Hailo or TensorRT, so custom kernels are needed;
  - newer SSM variants trade edge latency for cloud throughput;
  - distillation literature is dominated by RGB natural images. Distilling FM features into students for *non-RGB* modalities (thermal IR, event, RF spectrograms, GNSS correlator outputs) is barely explored;
  - few studies check whether distilled students keep the teacher's OOD robustness and calibration;
  - a capacity gap appears when the teacher-student size ratio is extreme (MCU scale), and the TinySSL preprint (§6) raises the same question for SSL methods.
- **Portability:**
  - Jetson/TensorRT: distilled ViT-S, MobileNet and EfficientNet run well.
  - Hailo: CNN students fit well, while ViT/SSM operator coverage is limited (not verified).
  - MCU: CNN students of ≤1 MB only; SSMs via custom TFLM kernels.
- **Defense coverage:**
  - Applied: navigation-oriented detection (EdgeNavMamba, generic robotics).
  - Not found: FM distillation for FPV/drone detection on MCUs, Mamba for RF/IQ or GNSS time-series interference classification on MCUs, or CLIP-style open-vocabulary detection of drones on Hailo/MCU. Sequence-modality defense signals (RF, acoustic, GNSS) fit SSMs well but appear untested.

### Gaps
- No 2024-2026 journal survey (Q1) of SSMs on edge/MCU was found. The evidence is preprints and a thesis.
- Hailo operator support for attention/SSM was not verified.

---

## 5. Uncertainty estimation and calibration on edge (evidential, conformal), open-set recognition, OOD detection

### Takeaway
Single-pass uncertainty for MCUs is an active 2024-2026 niche (L2): early-exit ensembles (QUTE), streaming conformal calibration (TCUQ), and next-activation prediction (SNAP-UQ, ICLR 2026). Conformal prediction is mature in theory (L4 statistically) but barely adapted to MCU streaming. The core gap is the exchangeability assumption under drift. Evidential learning is cheap but theoretically contested.

### Cited Findings
- **QUTE (2024, preprint):** uncertainty in TinyML via early-exit-assisted ensembles. Detects covariate-shifted and OOD inputs and is competitive with G-ODIN. It separates semantic shift (OOD) from non-semantic shift (corruption). — [arXiv 2404.12599](https://arxiv.org/html/2404.12599v1)
- **TCUQ (2025, preprint):** single-pass UQ from temporal consistency plus a *streaming conformal* layer that turns the score into a budgeted accept/abstain rule. It needs no online labels and no extra forward passes, and fits on kilobyte-scale MCUs with lower footprint and latency than early-exit or deep ensembles. Improves accuracy-drop detection by 3-7 AUPRC points, reaching up to 0.86 AUPRC at high corruption severity. — [arXiv 2508.12905](https://arxiv.org/abs/2508.12905v1)
- **SNAP-UQ (ICLR 2026):** single-pass, label-free UQ via self-supervised layer-to-layer next-activation prediction. Reduces flash and latency vs early-exit and deep ensembles, with failure-detection AUROC ≈0.9. — [ICLR 2026 poster](https://iclr.cc/virtual/2026/poster/10008878); [arXiv 2508.12907](https://arxiv.org/abs/2508.12907v4)
- **Anchors (not re-verified this session):**
  - Angelopoulos & Bates, "Conformal Prediction: A Gentle Introduction" (Foundations and Trends in ML, 2023). — [arXiv 2107.07511](https://arxiv.org/abs/2107.07511)
  - Sensoy et al., Evidential Deep Learning (NeurIPS 2018). — [arXiv 1806.01768](https://arxiv.org/abs/1806.01768)
  - Jürgens et al., "Is Epistemic Uncertainty Faithfully Represented by Evidential Deep Learning Methods?" (ICML 2024). A critique of EDL's epistemic validity. — [arXiv 2402.09056](https://arxiv.org/abs/2402.09056)
  - Yang, Zhou, Li, Liu, "Generalized Out-of-Distribution Detection: A Survey" (IJCV 2024). — [arXiv 2110.11334](https://arxiv.org/abs/2110.11334)

### Inferences
- **Maturity:**
  - Softmax/energy-score OOD on edge: L3. Free, single-pass.
  - Early-exit ensembles: L2.
  - Streaming conformal on MCU: L1-L2 (one preprint).
  - Evidential heads: L2 in practice, contested in theory.
  - Open-set recognition on MCU: L1. No MCU-specific OSR work found.
- **Methodological gaps:**
  - conformal guarantees assume exchangeability, which breaks under drift and adversarial jamming. Online/adaptive conformal on MCUs is nascent;
  - effect of INT8/sub-8-bit quantization on calibration is rarely measured;
  - evidential uncertainty may not faithfully represent epistemic uncertainty (ICML 2024 critique);
  - OOD benchmarks are image-centric, with no standard OOD benchmark for RF, GNSS or acoustic edge tasks;
  - coupling UQ to downstream decisions (abstain, wake a bigger model, request a label for continual learning) is mostly unexplored on-device.
- **Portability:** single-pass methods (softmax/energy, TCUQ, SNAP-UQ, evidential heads) port to MCU, Hailo and TensorRT because they add only small heads. MC-dropout and deep ensembles are impractical on MCUs, feasible on Jetson. Conformal calibration is a thresholding step that is trivially portable, but the calibration set must be stored or updated on-device.
- **Defense coverage:** no 2024-2026 work was found applying calibrated/conformal uncertainty or open-set recognition on edge hardware to drone/FPV detection (e.g., unknown drone models), GNSS interference (unknown jammer types), or RF emitter classification. These are inherently open-set problems.

### Gaps
- No 2024 paper specifically applying conformal prediction for OOD on MCUs was found. TCUQ (2025) is the closest.
- No edge OSR survey was located.

---

## 6. Test-time adaptation / domain adaptation on device; self-supervised learning for unlabeled sensor data

### Takeaway
On-device TTA reached MCUs in 2024: TinyTTA (NeurIPS 2024) on STM32H747 with 512 KB, using early-exit self-ensembles and no batch-norm reliance. 2025-2026 work pushes toward forward-only, integer-only TTA (FORGE) and on-device TTA benchmarking (BoTTA). SSL for sub-megabyte MCU models is an open question that 2026 preprints have only begun to address.

### Cited Findings
- **TinyTTA (NeurIPS 2024):** Jia, Kwon, Orsino, Dang, Talia, Mascolo (Cambridge / Calabria / Melbourne; author list from prior knowledge, affiliations from search). A self-ensemble, batch-agnostic early-exit TTA strategy for small batches, plus the TinyTTA Engine (an MCU library built on TFLM). Up to 57.6% better TTA accuracy and up to 6x lower memory. Validated on Raspberry Pi Zero 2W and STM32H747. Claimed to be the only framework running TTA on the STM32H747 under 512 KB. Code release was described as "coming soon". — [NeurIPS 2024 paper](https://papers.neurips.cc/paper_files/paper/2024/file/4c454d34f3a4c8d6b4ca85a918e5d7ba-Paper-Conference.pdf); [GitHub cam-mobsys/TTE](https://github.com/cam-mobsys/TTE)
- **FORGE (preprint, ID 2609.01683 not verified):** forward-only TTA for integer-only vision models on MCUs. It argues gradient-based TTA needs the stored activation graph and optimizer state of a floating-point model, which integer-only runtimes do not materialize. — [arXiv 2609.01683](https://arxiv.org/pdf/2609.01683)
- **BoTTA (2025, preprint):** benchmarks on-device TTA on Raspberry Pi 4B and Jetson Orin Nano, not MCUs. — [arXiv 2504.10149](https://arxiv.org/abs/2504.10149)
- **TinySSL (2026, preprint):** standard SSL methods (SimCLR, BYOL, DINO) were designed for backbones with tens of millions of parameters, so their effectiveness at MCU scale is an open question. Proposes distilled SSL pretraining for sub-MB MCU models (results not read). — [arXiv 2605.08241](https://arxiv.org/abs/2605.08241)
- **Deutel et al. (MCSoC 2025):** unsupervised VAE training on Cortex-M MCUs to learn image feature extractors, then classification heads from small labeled sets. Reduces labeled-data needs. — [FAU CRIS](https://cris.fau.de/publications/348030462)
- **Edge Learning Machine (Univ. of Genoa PhD thesis):** open-source framework with shallow, self-supervised and binary DL on constrained devices, including on-device SSL training on MCUs. — [UniGe IRIS](https://iris.unige.it/retrieve/a4bb0c5a-b5a3-4350-a3a8-0403ac5ae25c/phdunige_%204779788.pdf)
- **"Training on the Fly: On-device Self-supervised Learning aboard Nano-drones":** listed only by title in a curated list. — [awesome-tinyml](https://github.com/gauravfs-14/awesome-tinyml)
- **GNSS SSL example:** contrastive (dictionary-based) learning for GNSS jamming detection with edge-oriented compression. — [arXiv 2512.07512](https://arxiv.org/abs/2512.07512)
- **Anchor (not re-verified this session):** Liang, He, Tan, "A Comprehensive Survey on Test-Time Adaptation under Distribution Shifts" (IJCV). — [arXiv 2303.15361](https://arxiv.org/abs/2303.15361)

### Inferences
- **Maturity:** TTA on Jetson/RPi: L2-L3. TTA on MCU: L2 (one NeurIPS paper, code not fully public). Forward-only/integer TTA: L1. SSL pretraining for MCU-scale models: L1. On-device SSL: L1.
- **Methodological gaps:**
  - most TTA relies on BatchNorm statistics and large batches, which MCUs lack;
  - integer-only runtimes block gradient TTA;
  - TTA can collapse under continual or adversarial shift, so safety mechanisms (reset, UQ gating) are needed;
  - benchmarks are image-corruption based (CIFAR-C / ImageNet-C), not real sensor drift such as weather, sensor ageing or RF environment change;
  - SSL augmentations for RF/IQ, GNSS and acoustic data are not standardized;
  - SSL at sub-MB scale is unproven.
- **Portability:** MCU via TinyTTA Engine (TFLM-based) or forward-only approaches. Jetson is native. Hailo and Edge TPU are compiled, static graphs, so only forward-only/normalization-statistic TTA is plausible (inference, not verified).
- **Defense coverage:** drift is intrinsic in defense settings: day/night/thermal, weather, different drone airframes, changing RF environments, new jamming waveforms. Yet I found no on-device TTA work on drone/FPV detection, GNSS interference or RF sensing. The only domain example found is nano-drone on-device SSL (title only).

### Gaps
- FORGE metadata (authors, venue, exact arXiv ID) is unverified.
- The TinySSL results were not read.

---

## 7. Multimodal sensor fusion under compute limits; early-exit / dynamic inference; energy-aware scheduling

### Takeaway
Dynamic inference (early exit, skipping, adaptive modality selection) is mature as a concept (L3; TPAMI 2022 survey) and was reframed in 2025 for multimodal sensor fusion. Energy-harvesting-aware and QoI-aware multimodal adaptation are L1-L2. Defense edge sensing (acoustic drone detection on STM32) exists, but mostly as single-modality, non-adaptive pipelines.

### Cited Findings
- **Survey (2025, revised Feb 2026, preprint):** Montello et al., "A Survey on Dynamic Neural Networks: from Computer Vision to Multi-modal Sensor Fusion". Taxonomy by which component adapts: output, computation graph or input. Argues dynamic networks suit multimodal fusion. — [arXiv 2501.07451](https://arxiv.org/abs/2501.07451)
- **ADMN (2025, preprint):** layer-wise adaptive multimodal network for dynamic input noise and compute budgets. Standard early exiting ignores multimodal quality-of-information (QoI)-aware resource allocation. — [arXiv 2502.07862](https://arxiv.org/abs/2502.07862)
- **Energy-aware multi-exit ViT (journal, Qom):** for energy-harvesting edge devices, inference terminates at intermediate layers depending on available energy. The 4th exit gives a 28.5% FLOPs reduction. — [JEMSC](https://jemsc.qom.ac.ir/article_3860.html) (low-tier venue; quartile unverified)
- **Adaptive AI multi-exit TinyML for vision at the edge (preprint):** — [arXiv 2609.11939](https://arxiv.org/abs/2609.11939) (details not read)
- **Early-exit survey (NLP, 2025):** deployment on resource-constrained edge/IoT devices remains a central challenge. — [arXiv 2501.07670](https://arxiv.org/html/2501.07670v1)
- **Early exit reused for UQ and TTA:** QUTE (§5) and TinyTTA (§6) both repurpose early exits, so dynamic inference is becoming a shared substrate for robustness. — [QUTE](https://arxiv.org/html/2404.12599v1); [TinyTTA](https://neurips.cc/virtual/2024/poster/94778)
- **Defense acoustic edge examples:**
  - Embedded AI on STM32 for audio-based drone detection at railway infrastructure (Transport Problems, 2025). — [repository](https://crust.ust.edu.ua/handle/123456789/21689)
  - University of Dayton MS thesis (2024): a TinyML drone detector on a low-cost MCU with an integrated microphone. — [eCommons](https://ecommons.udayton.edu/graduate_theses/7478)
  - TinyML acoustic event detection on sensor nodes improves energy efficiency and node lifetime (JTIT 2025, not drone-specific). — [ITL repository](https://bc.itl.waw.pl/publication/2714)
- **Anchor (not re-verified this session):** Han et al., "Dynamic Neural Networks: A Survey", IEEE TPAMI 44(11), 2022. — [arXiv 2102.04906](https://arxiv.org/abs/2102.04906)

### Inferences
- **Maturity:** early exit on MCU: L2-L3. Multimodal adaptive fusion: L1-L2. Energy-harvest/battery-aware scheduling of DNN inference: L1-L2. Cascades (wake-up tiny model → heavier model): L3 in practice (e.g., always-on KWS), but rarely formalized for multimodal defense sensors.
- **Methodological gaps:**
  - exit-policy learning that accounts for sensor-quality degradation (QoI);
  - joint modality selection and exit under an energy budget;
  - calibration of exit confidence (overconfident early exits);
  - real-hardware energy measurement instead of FLOPs proxies;
  - dynamic graphs are poorly supported by static compilers (TFLM, Hailo, TensorRT need fixed graphs or multiple engines);
  - no benchmarks for asynchronous multimodal streams (acoustic + RF + EO/IR) at MCU scale.
- **Portability:** early exits can be compiled as multiple sub-graphs on MCU, Hailo or TensorRT. True input-dependent dynamic routing is hard on NPUs. Heterogeneous scheduling (MCU always-on + NPU/Jetson on demand) is a system-level pattern rather than a toolchain feature.
- **Defense coverage:**
  - Applied: single-modality acoustic drone detection on STM32. Multi-sensor drone detection datasets exist (e.g., Svanström et al. IR/visible/audio dataset; not re-verified this session).
  - Not found: compute-adaptive multimodal fusion for drone detection at MCU scale, or energy-aware scheduling for persistent unattended sensing nodes in defense. RF-based edge drone detection did not surface in this session's search.

### Gaps
- RF drone detection on edge hardware was not covered by this session's searches.
- No Q1 journal survey specifically on energy-aware scheduling for TinyML was found.

---

## 8. Hyperdimensional computing (HDC / vector symbolic architectures) as a low-power alternative

### Takeaway
HDC offers one-shot/few-shot learning, trivially cheap on-device updates (vector bundling) and noise tolerance. The foundational surveys are ACM Computing Surveys (2022-2023), while 2024-2026 work focuses on hardware (ASIC/FPGA/in-memory) and compression (DPQ-HD). Maturity is L2. The accuracy gap vs DNNs on raw high-dimensional signals (images, IQ) persists, and most systems still need a learned feature extractor.

### Cited Findings
- **Foundational surveys:** Kleyko, Rachkovskij, Osipov, Rahimi, "A Survey on Hyperdimensional Computing aka Vector Symbolic Architectures, Part I: Models and Data Transformations", ACM Computing Surveys 55(6), 2022/2023, pp. 1-40. Part II covers applications, cognitive models and challenges. — [arXiv 2112.15424 (Part II)](https://arxiv.org/abs/2112.15424) (ACM CSUR: Q1, generally known; DOI not re-verified)
- **AICAS 2024:** Hassan, Bettayeb, Mohammad, "Advancing Hardware Implementation of Hyperdimensional Computing for Edge Intelligence" (pp. 169-173). Analyzes HDC on ASIC, CPU and FPGA. Short paper. — [Khalifa Univ.](https://khazna.ku.ac.ae/en/publications/advancing-hardware-implementation-of-hyperdimensional-computing-f/)
- **DPQ-HD (2025, preprint):** post-training compression for ultra-low-power HDC. — [arXiv 2505.05413](https://arxiv.org/abs/2505.05413)
- **"Revisiting HyperDimensional Learning for FPGA and Low-Power Architectures" (DGIST):** — [DGIST](https://dgist.elsevierpure.com/en/publications/revisiting-hyperdimensional-learning-for-fpga-and-low-power-archi/)
- **LookHD (HPCA 2021):** real-time HDC learning on low-power edge devices (via search summary; older). — [NSF PAR](https://par.nsf.gov/servlets/purl/10334215)

### Inferences
- **Maturity:** L2. Strong on biosignals (EMG/EEG), language ID and simple sensor classification. Weaker on vision and RF. Hardware prototypes exist, but there is no mainstream toolchain (TFLM, STM32Cube.AI, Hailo and TensorRT do not target HDC; it runs as plain C code on MCUs).
- **Methodological gaps (from the Part II challenges and the 2024-2025 hardware focus):**
  - encoding design (how to map raw continuous/time-series signals into hypervectors) is ad hoc;
  - accuracy gap vs DNNs on complex data;
  - hybrid DNN-feature + HDC-classifier designs lack principled training;
  - limited theory for capacity vs dimensionality under quantization;
  - few standardized benchmarks vs MLPerf Tiny.
- **Portability:** excellent on MCUs (bitwise ops, binary/bipolar vectors), FPGAs and in-memory computing. NPUs (Hailo, TensorRT) are not a natural fit beyond the feature extractor.
- **Defense coverage:** no 2024-2026 HDC application to drone/FPV detection, GNSS interference or RF sensing nodes was found in this session. HDC's one-shot class addition and on-device update properties overlap directly with the open-set and continual-learning gaps in §1 and §5.

### Gaps
- No 2024-2026 Q1 journal survey on HDC for edge/TinyML was found in this session's searches.
- No HDC few-shot defense application was found.

---

## 9. Cross-cutting map: methods × defense-relevant problems (what has / has NOT been applied)

### Takeaway
Across all eight method families, defense-relevant evidence on edge hardware clusters in two places. The first is event/neuromorphic drone detection (FOI 2025 tripwire; counter-UAV event-vision survey 2025). The second is compressed static classifiers for GNSS jamming (2025-2026 preprints) and acoustic drone detection on STM32. The adaptive methods (on-device CL/TTA, calibrated/open-set UQ, SSL, FM distillation to MCU, SSMs, HDC) show no defense-specific edge applications in the sources found.

### Cited Findings
- Drone detection with event camera + SNN + neuromorphic chip, about 1000x+ more energy-efficient than an edge GPU. — [arXiv 2509.12997](https://arxiv.org/abs/2509.12997v1)
- Counter-UAV event-camera survey: detection, tracking, forecasting, propeller-signature identification. — [alphaXiv 2508.04564](https://alphaxiv.org/overview/2508.04564v1)
- GNSS jamming detection compressed for edge (contrastive + pruning + distillation). — [arXiv 2512.07512](https://arxiv.org/abs/2512.07512)
- GNSS jamming/spoofing classification with an 8-bit VAE on Edge TPU (2026). — [arXiv 2605.14839](https://arxiv.org/abs/2605.14839)
- Crowdsourced edge GNSS interference detector (ENC 2025, Thales) using statistics + fuzzy logic rather than DL. >75% jamming and 95% spoofing precision, ~1-2% false positives, ~10 s mean detection time. — [search result via sciforum](https://sciforum.net/paper/view/25272) (attribution to Thales/ENC 2025 is from the search summary; not verified)
- Acoustic drone detection on STM32 (2025) and MCU-microphone TinyML (2024 thesis). — [Transport Problems](https://crust.ust.edu.ua/handle/123456789/21689); [Dayton thesis](https://ecommons.udayton.edu/graduate_theses/7478)
- Navigation-oriented Mamba detector on Jetson/RPi. — [arXiv 2510.14946](https://arxiv.org/html/2510.14946v1)
- On-device SSL on nano-drones (title only). — [awesome-tinyml](https://github.com/gauravfs-14/awesome-tinyml)

### Inferences
- **Applied (some evidence):**
  - neuromorphic/event → drone detection;
  - quantization/pruning/distillation → GNSS jamming and acoustic drone detection;
  - Mamba + KD → navigation detection on Jetson.
- **Not found in this session (white space):**
  - on-device continual/few-shot learning for new drone types, jammer waveforms or RF emitters;
  - conformal/evidential UQ or open-set recognition on edge for any defense task;
  - on-device TTA for EO/IR drone detection under weather or day/night shift;
  - SSL on unlabeled RF/GNSS/acoustic streams at MCU scale;
  - FM (DINOv2/CLIP/SAM) distillation into MCU or Hailo detectors for FPV/drone;
  - SSMs for RF/GNSS sequences on MCUs;
  - HDC for any defense sensing;
  - neuromorphic processing of RF or GNSS signals;
  - energy-aware multimodal (acoustic + RF + EO) adaptive fusion for persistent unattended sensing nodes;
  - visual navigation (GNSS-denied) evaluated on MCU/neuromorphic hardware.
- **Evidence quality caution:** most defense-specific edge evidence is preprints or theses (L1-L2 evidence tier), not Q1 journals. Q1 coverage is concentrated in general method surveys (Nature 2025 neuromorphic; TPAMI event vision, dynamic networks; IJCV OOD, TTA; ACM CSUR HDC).

### Gaps
- Absence of evidence ≠ evidence of absence. Searches were limited (about 15 queries). Defense work is often unpublished or classified, and RF-based drone detection on edge, visual navigation on MCUs, and persistent-node scheduling were not specifically searched.
- Scimago quartiles were not checked directly on scimagojr.com in this session. Only well-known venues (Nature, TPAMI, IJCV, ACM CSUR) are noted as Q1, from general knowledge.
