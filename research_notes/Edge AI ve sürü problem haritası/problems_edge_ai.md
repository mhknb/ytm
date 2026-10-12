# Open application problems for low-power / edge AI (TinyML, Edge AI) in defense, 2024-2026

Scope note: these notes map defense application problems, not methods. Four problem areas are used throughout:
- **P1**: Detecting and classifying small drones and FPV kamikaze drones on low-power, portable, soldier-worn or distributed sensors. Sub-problems: bird vs drone, and RF-silent drones (fiber-optic FPV, autonomous or "sleeper" drones).
- **P2**: Always-on sensing on battery-powered nodes (unattended ground sensors, perimeter, acoustic and seismic).
- **P3**: Onboard perception on small UAVs under SWaP limits. This includes the onboard perception of interceptor drones and terminal-guidance drones.
- **P4**: On-device threat and anomaly detection for UAVs (GNSS interference, onboard bus intrusion). P4 is covered only briefly, as instructed.

Quartile note: I could not check Scimago quartiles live. Where a quartile is given, it comes from general knowledge and is marked "SJR unverified".

---

## Q1. Why these problems matter now: field evidence and defense relevance

### Takeaway
Small FPV and one-way drones are now a main cause of attrition in Ukraine. This creates a mass, low-cost threat. Expensive, centralized, emitting sensors (big radars, missiles) cannot cover it, so the answer must be cheap, passive, distributed and often man-portable sensing with local (edge) intelligence.

Two developments in 2024-2026 broke the most common cheap detector, the RF scanner:
- fiber-optic FPVs, which emit no RF at all;
- autonomous terminal guidance, which keeps a drone on target after its link is lost.

Ukraine's acoustic network (Sky Fortress, about 10,000 nodes at a few hundred dollars each) is the strongest field proof that distributed low-cost edge-ML sensors work at national scale.

### Cited Findings

**Scale of the drone threat**
- RUSI (Feb 2025): tactical UAVs "currently account for 60–70% of damaged and destroyed Russian systems". Between 60 and 80% of Ukrainian FPVs fail to reach their target. Ukrainian brigades report that "approximately 50% of their casualties are taken in the rear from Russian FPVs, artillery and glide bombs". The same report notes that "the scale of wire-guided FPV employment and density of persistent ISR" has made resupply, casualty evacuation and concealment harder. — [RUSI, Tactical Developments During the Third Year of the Russo-Ukrainian War (Feb 2025)](https://static.rusi.org/tactical-developments-third-year-russo-ukrainian-war-february-2205.pdf). The authors are Jack Watling and Nick Reynolds to my knowledge; the PDF metadata returned "Alice Trouncer", so the attribution is unverified.
- ISW (Aug 2025), citing EW expert Serhiy "Flash" Beskrestnov and an unnamed medical facility: "70 percent of the injuries sustained by Ukrainian forces and civilians result from FPV drone attacks along Ukrainian highways" in the Pokrovsk direction. This is a second-hand figure. — [ISW special report, Russian Drone Innovations and BAI (Aug 2025)](https://understandingwar.org/research/russia-ukraine/russian-drone-innovations-are-likely-achieving-effects-of-battlefield-air-interdiction-in-ukraine/)
- Ukraine produced about 2 million drones in 2024, including more than 1.5 million FPVs. — [CSIS, Ukraine's Future Vision and Current Capabilities for AI-Enabled Autonomous Warfare](https://www.csis.org/analysis/ukraines-future-vision-and-current-capabilities-waging-ai-enabled-autonomous-warfare). CSIS interview participants also cited 0.8M drones in 2023, 2M in 2024 and up to 5M planned for 2025 — [CSIS, The Russia-Ukraine Drone War](https://www.csis.org/index%2Ephp/analysis/russia-ukraine-drone-war-innovation-frontlines-and-beyond).
- Russian salvos grew from about 100 to nearly 300 weapons per wave by 2025, and the gap between salvos shrank to 8 days. Shahed hit rates roughly doubled, from under 10% to about 20%, partly because the drones now fly at higher altitude, "exploiting radar gaps". — [CSIS, The New Salvo War](https://www.csis.org/index%2ephp/analysis/new-salvo-war)

**RF-silent drones break RF detection (the fiber-optic gap)**
- NATO ACT's 16th Innovation Challenge (June 2025) was dedicated to detecting, tracking and neutralizing fiber-optic FPVs, which were "first documented in Russian deployments in late 2024".
  - Standard C-UAS "which depend on jamming or signal spoofing, have proven ineffective".
  - Requirements: detection by radar, thermal, acoustic or optical sensors; total weight under 100 kg; day and night in adverse weather; 500 m detection range; cost-effective for near-term deployment in Ukraine.
  - The challenge drew 162 proposals, 42 of them Ukrainian.
  - [NATO ACT (24 Jun 2025)](https://www.act.nato.int/article/innovation-challenge-fibre-optic-drones/)
- ISW: Ukrainian servicemen say their "only effective countermeasures against Russian fiber optic UAVs are small arms". Ukraine needs "new radars and ways of identifying UAVs, such as sleeper and fiber optic UAVs, which do not emit radio-frequency signals". Ukrainian truck-mounted EW is losing effectiveness because "Russian FPV drones are operating on a wider range of frequencies". — [ISW special report (Aug 2025, PDF)](https://understandingwar.org/wp-content/uploads/2025/08/Russian20Drone20Innovations20and20BAI2C20August2072C20202520220PDF.pdf)
- Analyst Rob Lee is cited as saying that in some Russian units up to 50% of FPVs use optical fiber. Personal RF detectors have "a much harder time" with these drones. An Azovets EW platoon commander wants detection coverage from "200 MHz to 15 GHz". — [Euromaidan Press via uazmi (May 2026)](https://uazmi.com/news/post/a2e1d04d1babe9da891c8b20a4be6f31). This is media reporting of practitioner statements.
- US CJCS Gen. Dan Caine said US forces should assume they will be "hunted by autonomous systems, jammed across the spectrum". He said FPVs with AI-enabled computer vision "can now continue toward targets even when GPS signals or control links are disrupted". In other words, RF links disappear in the terminal phase. — [Jerusalem Post (Oct 2026)](https://www.jpost.com/defense-and-tech/article-910744)
- CSIS: AI-based autonomous navigation raises strike success from "around 10 to 20 percent to around 70 to 80 percent". Onboard ATR has extended target recognition "from 300 meters to an average of 1 km in combat and to up to 2 km". — [CSIS](https://www.csis.org/analysis/ukraines-future-vision-and-current-capabilities-waging-ai-enabled-autonomous-warfare)

**Soldier-level detection demand**
- Wearable RF detectors are now in wide frontline use: MyDefence/Autonomous Guard Wearable Kit, SkyLock Sky Spotter Pro, Obriy 1.3. The Obriy 1.3 monitors 1.2, 2.4 and 4.9–6.0 GHz with a typical range of 2.5 km. The US Army C5ISR Center "has been researching radio-frequency and acoustic detection systems for dismounted soldiers". — [The Defense News (Jun 2026)](https://www.thedefensenews.com/Battlefield-Tested-Ukrainian-Obriy-13-Drone-Detector-Seen-During-US-Army-Training-Exercise/); [Jerusalem Post](https://www.jpost.com/defense-and-tech/article-910744)
- The MyDefence Wingman wearable RF detector weighs 1,100 g, runs 10–14 h on a battery and senses 200 MHz–6 GHz passively. These figures show the SWaP envelope of a fielded soldier-worn detector. It is still RF-only. — [MyDefence product page](https://mydefence.com/wearable-solutions/wingman-drone-detector/)

**Distributed acoustic edge-ML works at scale (Sky Fortress)**
- Sky Fortress has about 9,500 acoustic nodes. Each costs about $400–500 (the first versions cost about $300: a phone and microphone on a 2 m pole). An 84-UAV salvo was reduced to 4 leakers. Romania could be covered for about $6M. — [Defense One (Jul 2024)](https://www.defenseone.com/defense-systems/2024/07/ukraines-cheap-sensors-are-helping-troops-fight-waves-russian-drones/398204/); [FlightGlobal (Sep 2024)](https://www.flightglobal.com/military-uavs/2024/09/how-ukraine-turned-mobile-phone-microphones-into-an-air-defence-network/)
- US Army CALL, "Listening to the Sky" (No. 26-1115, Mar 2026, analyst Joseph Serowik):
  - Ukrainian acoustic nodes "locally classify events with edge machine learning (ML)" and send compact records (bearing, confidence, node ID, timestamp) rather than raw audio.
  - Typical effective range against small quadcopters or FPVs is "hundreds to a few thousand meters".
  - Limits: wind, temperature gradients, urban noise, quiet electric propulsion.
  - The report recommends adopting the approach on NATO's Eastern Flank and in INDOPACOM.
  - [CALL PDF](https://api.army.mil/e2/c/downloads/2026/04/30/af450e75/no-26-1115-listening-to-the-sky-acoustic-drone-detection-in-ukraine-mar-26.pdf)
- More than 10,000 Sky Fortress sensors are reported as of 2026. As of April 2026 the platform had been deployed by the US military at Prince Sultan Air Base against Shaheds. — [Wikipedia, Sky Fortress](https://en.wikipedia.org/wiki/Sky_Fortress_(drone_defense_system)). This is a secondary source.

**Mass drones need cheap sensors**
- CSIS: each Shahed costs about $20,000–50,000, against SAM interceptors costing several hundred thousand dollars. Ukraine fielded "tens of thousands of acoustic sensors" and the DELTA common operating picture. — [CSIS, Drone Saturation](https://www.csis.org/analysis/drone-saturation-russias-shahed-campaign)

### Inferences
- The defense "demand signal" for edge AI is strongest in P1. It needs cheap passive sensors (acoustic, optical/thermal, event cameras, low-cost radar) that work when RF is absent, with on-node classification so that only compact alerts are sent. Two reasons for alerts-only: bandwidth, and operational security against emitter triangulation.
- The RF-only wearable detector is the fielded baseline. Its blind spot is fiber-optic FPVs, autonomous terminal phases and "sleeper" drones. This gap is explicitly stated by NATO, ISW and practitioners.
- P2 (UGS) and P1 are converging. The same battery-powered node may need to listen for drones, vehicles and footsteps at once.

### Gaps
- I found no official NATO or RUSI quantitative estimate of the share of fiber-optic FPVs across the whole front. Only anecdotal "up to 50% in some units" figures exist.
- No public, quantified field performance data (Pd/Pfa vs range) exist for soldier-worn non-RF detectors.

---

## Q2. What current solutions do and exactly where they fall short (open challenges from 2024-2026 reviews)

### Takeaway
Across 2024-2026 reviews, the same gaps recur:
- lab-to-field generalization (noise, weather, domain shift);
- tiny or distant targets, and birds and other distractors;
- real-time inference on edge hardware, which is named as a future direction but rarely demonstrated;
- multi-sensor fusion that is "still in early stages";
- no standard benchmarks or shared evaluation protocols.

Power budgets, multi-drone scenes, RF-silent drones and adversarial robustness are named as open problems but almost never tested on real low-power hardware.

### Cited Findings

#### P1 — Small drone / FPV detection: cross-modal review findings

- **Dong et al., "Securing the Skies…" (CVPR 2025 Workshops)**
  - The analysis "reveals persistent gaps in real-time performance, stealth detection, and swarm-based scenarios".
  - Section 2 (datasets) finds "persistent gaps in annotation standards, sensor synchronization, and adversarial realism". It calls for datasets on "night-time operations, swarm-based threats, and real-time interception".
  - Section 3 ("Key Insights & Challenges"), modality by modality:
    - RF is hurt by "radio congestion and potential adversarial attacks";
    - audio "suffer[s] from significant performance drops in high-noise or windy environments";
    - radar has "higher costs and calibration demands";
    - vision "degrade[s] with lighting or weather changes";
    - fusion "raises complexity in real-time deployment".
  - Also: "adversarial robustness remains an open problem", and "a continuing research direction involves efficient, low-latency architectures … for on-board or edge-based processing".
  - [CVF open access PDF](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf)
- **Mrabet, Sliti, Ben Ammar (Frontiers in Communications and Networks, 2024)**
  - "Much of the research in this field is experimental, making it difficult to compare results"; "noteworthy lack of reference datasets".
  - "Most proposed solutions are grounded in static detection setups", which is a problem in cluttered urban areas. The authors propose "distributed and collaborative detection systems".
  - Per-modality future work repeatedly calls for "lightweight and efficient algorithms that can operate on edge devices". For acoustics, "many existing systems struggle with processing speed" and "current datasets often lack representation of various drone types and operational conditions".
  - [Frontiers](https://www.frontiersin.org/journals/communications-and-networks/articles/10.3389/frcmn.2024.1440727/full)
- **Seidaliyeva et al. (Sensors 2024, 24(1):125)**
  - Detection difficulty stems from the "size and speed diversity of drones, their dynamic behavior and similarity to other flying objects".
  - Real-world interference: weather, lighting, urban obstructions, wind, Wi-Fi and Bluetooth signals, "bird echoes".
  - Bimodal and multimodal fusion methods "are still in the early stages of development and implementation".
  - [MDPI](https://www.mdpi.com/1424-8220/24/1/125)
- **Rahman et al. (Remote Sensing 2024, 16(5):879)**: a per-modality "Challenges and Solutions" and "Future Directions" structure (Sections 2.1.1–2.4.2). Every modality's future direction lists multisensor fusion. The radar section adds the need to "distinguish UAVs from other objects". — [MDPI](https://www.mdpi.com/2072-4292/16/5/879)
- **Semenyuk et al. (Int. J. Critical Infrastructure Protection, vol. 49, 2025, DOI 10.1016/j.ijcip.2025.100744)**: reviews 2020–present multi-sensor and AI UAV detection with emphasis on fusion. I read only the abstract, so challenge items are not extracted. — [RePEc entry](https://ideas.repec.org/a/eee/ijocip/v49y2025ics1874548225000058.html)
- **Metalidi, Belyakov, Kovalchuk (2026; Ukrainian journal, "Communication informatization and cybersecurity systems and technologies")**
  - States that fiber-optic platforms "are effectively immune to electronic warfare systems and 'invisible' to RF detectors, thereby creating a critical gap".
  - RF methods "are fundamentally unsuitable for autonomous and fiber-optic platforms".
  - Radar range "drops sharply" as RCS decreases.
  - Acoustics suffer "elevated false alarm rates in urban noise".
  - EO/IR "need[s] external cueing due to the limited field of view".
  - The paper is conceptual only; it has no dataset or experiment.
  - [Exa library entry](https://exa.ai/library/publication/qd3q7bhzw45)

#### P1 — Acoustic detection (most edge-friendly modality)

- **Kang et al. (AIP Advances 15(12):120701, Dec 2025)**: "Current drone acoustic detection research faces challenges such as limited annotated data, uneven distribution, and scenario homogeneity". Section VI covers future directions. Table II lists 7 open acoustic datasets, the largest being 33,090 s for localization. — [AIP](https://pubs.aip.org/aip/adv/article/15/12/120701/3373725/From-classical-approaches-to-recent-advancements-A)
- **Altujar et al., "A Review of Acoustic Techniques for Drone Detection" (Nov 2025; venue not verified)**: "challenges remain in scalability, dataset generalizability, and computational efficiency". SVMs suit small datasets and low compute; CNNs need more resources. — [entry](https://exa.ai/library/publication/37xcx9hkxdf)
- **Ghouli (Acta Acustica, 2026)**
  - Open challenges: "Few studies address power constraints and real-time requirements necessary for embedded or autonomous deployment. Additionally, the classification of multiple drones, identification of drone types, and 3D localization remain open problems."
  - Their MEMS array on a Raspberry Pi reached only about 60 m effective range, with 91.6% accuracy up to 50 m.
  - Coastal wind cut sensitivity by 10–15%. Birds and vehicles caused a 5–8% false-positive rate. Overhead flights increased error by 20–25%.
  - [Acta Acustica](https://acta-acustica.edpsciences.org/articles/aacus/full_html/2026/01/aacus250134/aacus250134.html)
- **Blass & Graf (Forum Acusticum 2025, Fraunhofer-type mobile array work)**
  - "Most of the existing acoustic systems are stationary". Mounting arrays "on vehicle roofs or soldier helmets" is proposed.
  - Their 32-mic, 1 m dome draws about 120 W on an Intel NUC. Sub-arrays of 11 or more mics match the 32-mic baseline (median DOA error about 5° fixed, about 20° on a moving vehicle).
  - A helmet-scale version (0.25 m aperture) is only simulated.
  - [PDF](https://dael.euracoustics.org/confs/fa2025/data/articles/000269.pdf)
- **Microphone hardware study (Sensors 2025; PMC12656299)**
  - Public UAV acoustic datasets "remain limited in terms of platform variety, environmental diversity, and labeling consistency".
  - Low-power MEMS microphones (−40 to −45 dBV/Pa, 30–35 dBA self-noise) "limit detection capability at greater distances". Most works use MEMS "without providing systematic justification".
  - [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12656299/)
- **Aero EDIH / CAE / Monava field tests (May–June 2025)**: a MEMS array detected micro quadcopters at 200 m (±1°) and fixed-wing at 400 m. Advice: do not "rely solely on acoustic technology". — [Aero EDIH](https://www.aeroedih.eu/news/acoustic-drone-detection/). This is a project news item, not peer-reviewed.
- **Fiber-optic FPI and EFPI acoustic sensors** (IEEE Sensors J. 2024 and 2026, Harbin Engineering University group): DJI Mini3 detected at 200 m with 99.24% accuracy. These are lab-grade optical interrogators, not low-power. — [entry](https://exa.ai/library/publication/r16nghj48r2); [entry](https://exa.ai/library/publication/jkt05h7gmdb)
- **TinyML on a microcontroller for drone audio**: the only direct example I found is an MSc thesis (Mays, Univ. of Dayton, 2024), "Drone Detection Using Tiny Machine Learning", with a battery-powered MCU and microphone. — [eCommons](https://ecommons.udayton.edu/graduate_theses/7478/). I found no peer-reviewed 2024–2025 journal paper on MCU-class acoustic drone detection; this itself signals a gap.

#### P1 — RF detection

- **RFUAV (arXiv 2503.09033, 2025)**
  - Existing RF datasets "feature a restricted variety of drone types and insufficient volumes of raw data"; "lack raw data covering a broad range of SNR"; "do not offer open-access evaluation tools".
  - DroneRF covers only 3 drones "whereas the market offers over 60 distinct models". DroneRFa has about 25 types but no per-packet SNR.
  - RF methods "lack widely accepted baseline models and benchmark dataset".
  - [arXiv HTML](https://arxiv.org/html/2503.09033)
- MMAUD authors: "Some drones don't emit RF signals, making RF detection unreliable". — [ar5iv](https://ar5iv.labs.arxiv.org/html/2402.03706)
- Field limits:
  - frequency agility (practitioners ask for 200 MHz–15 GHz coverage);
  - co-located jammers interfere with and can "burn out" detectors;
  - next-gen detectors plan to add AI classification "and more layers of detection … visual and acoustic".
  - [Euromaidan via uazmi](https://uazmi.com/news/post/a2e1d04d1babe9da891c8b20a4be6f31)

#### P1 — Radar (micro-Doppler), including bird vs drone

- Micro-Doppler is the key cue for telling drones from birds and for spotting hovering drones. However:
  - "the lack of real-world data makes improving classification efforts difficult" ([Tsang et al., Signals 2023](https://www.mdpi.com/2624-6120/4/2/18); their data are "not publicly available due to sponsor restrictions");
  - "Real MDIs of multiple drones and birds are difficult to obtain", so a 2022 IEEE Access study relied on simulation ([IEEE Access 2022](https://ieeexplore.ieee.org/ielx7/6287639/9668973/09724239.pdf)).
- A W-band study notes that classification thresholds sit "very close to the noise floor", which "requires … a very low phase noise radar". That conflicts with cheap, low-power radar. — [SPIE / St Andrews](https://research-repository.st-andrews.ac.uk/bitstream/handle/10023/18319/110030S.pdf?isAllowed=y&sequence=1)
- Low-cost 24 GHz FMCW modules detected an off-the-shelf drone at only about 14 m (undoped). This illustrates the small-RCS problem for cheap radars. — [Maya et al. 2025 (ResearchGate)](https://www.researchgate.net/publication/393741936_Evaluation_of_Additive_Manufacturing_Techniques_to_Increase_Drone_Radar_Detection_Range)
- LSS-FMCWR-2.0 (2025) reports fusion gains of +12.3% at low SNR (−3 dB). This shows that accuracy collapses at low SNR. — [entry](https://exa.ai/library/publication/xbms8cydhz5)
- Practitioner literature claims that passive SDR radar (using DVB-T, GSM or LTE illumination) plus micro-Doppler CNNs can reveal fiber-optic FPVs. Range is limited by "the computational capabilities available at the receiver end". — [Samuel Bendett, LinkedIn (Apr 2026)](https://www.linkedin.com/posts/samuel-bendett-06996018_%D0%B2%D0%BE%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F-%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA%D0%B0-activity-7445198568975478786-dyP8). This is a weak source: a translated Russian milblogger summary. It indicates direction only.

#### P1 — Vision, IR and event cameras; bird vs drone

- Drone-vs-Bird (2020 edition, Sensors 2021): the hardest cases are "moving cameras and detection of distant drones". Algorithms "do not explicitly take birds into account … data are not annotated for birds", so flocks increase false alarms. "The appearance of distant fixed-wing UAVs is very similar to birds." — [Coluccia et al., Sensors 21(8):2824](https://www.mdpi.com/1424-8220/21/8/2824)
- The 8th Drone-vs-Bird challenge (IJCNN 2025) received 16 algorithms. "The variability of the results underscores the complexity of the task." — [Coluccia et al. 2025](https://exa.ai/library/publication/r45j7rqhssh)
- The winning 2025 entry used a medium-size YOLOv11 with multi-scale tiling, which is not edge-class. Per-video mAP50 ranged from 0.45 to 0.99 (average 0.739 on validation). Hillside backgrounds with rocks "closely mimic small-scale drones". — [arXiv 2504.19347](https://arxiv.org/html/2504.19347)
- Thermal tracking:
  - CST Anti-UAV (ICCV 2025 Workshops): the best SOT tracker achieves "only 35.92% state accuracy, much lower than the 67.69% observed on the Anti-UAV410 dataset".
  - Anti-UAV410 lacks "truly complex urban areas with dynamic distractors". Its "number of tiny objects is too limited".
  - [CVF PDF](https://openaccess.thecvf.com/content/ICCV2025W/Findings/papers/Xie_CST_Anti-UAV_A_Thermal_Infrared_Benchmark_for_Tiny_UAV_Tracking_ICCVW_2025_paper.pdf)
- IR-on-edge "trilemma": detection systems struggle to achieve small-target accuracy, real-time speed and resource-limited deployment at the same time. UAVs often appear as fewer than 100 pixels, with low contrast during thermal crossover. Dataset issues: few IR images, few small targets, limited UAV-type diversity, and bounding boxes too coarse. — [Chen et al., PLOS One 2025](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0330074)
- Event cameras:
  - On FRED, YOLO reaches mAP50 87.68 on event frames versus 35.24 on RGB.
  - All detectors drop on the "challenging split" (low light, insects, weather), and fusion "does not yet surpass the strongest event-only baseline".
  - [FRED, arXiv 2506.05163](https://arxiv.org/pdf/2506.05163v1.pdf)
  - Earlier propeller-frequency methods work well only "when observed from below" — [same](https://arxiv.org/pdf/2506.05163v1.pdf).
  - A low-power event+RGB setup on a Jetson Xavier NX (Mandula et al., I2MTC 2024) "does not report quantitative results" — as cited in [FRED](https://arxiv.org/pdf/2506.05163v1.pdf).
  - Frequency-cue gating (ICMR 2026) shows generalization gaps on unseen backgrounds (+74.8 AP50 gain needed in hard scenes). — [ACM DL](https://dl.acm.org/doi/10.1145/3805622.3810721)

#### P2 — Persistent and always-on sensing (UGS, perimeter, acoustic/seismic)

- Commercial UGS already detect footsteps, vehicles and digging with seismic, acoustic and PIR sensors:
  - batteries rated up to 12 months (rechargeable) or about 6 years (primary) ([SensoGuard](https://sensoguard.com/ugs-system-unattended-ground-sensors));
  - "radio silence" store-and-forward ([Exensor Mini Mk3](https://www.exensor.com/products/flexnet-flexible-network-of-sensors/unattended-ground-sensors-ugs/mini-mk3/));
  - seismic is the most common UGS modality ([DSIAC UGS survey, 2018](https://dsiac.dtic.mil/technical-inquiries/notable/unattended-ground-sensor-survey/)).
  - These are vendor claims, not independently tested.
- HyMAD (arXiv 2511.14698, 2025): "accurately detecting and distinguishing between overlapping activities that are happening simultaneously, such as human intrusions, animal movements, and vehicle rumbling, remains a major challenge". Its multi-activity samples were synthesized by superposition, not recorded. — [arXiv](https://arxiv.org/html/2511.14698)
- An Indian Army-oriented paper says border intrusion systems have had "limited success as far as system deployment in Indian Army is concerned". LoRa transmission "consumes more power", so alerts are sent periodically. — [VIBERSHIELD (2023)](https://exa.ai/library/publication/jwcfrqlqc84)
- Neuromorphic and low-power directions: LMU-based geophone classification (footsteps, vehicle, noise) reached 93.88% versus 95.15% for LSTM, motivated by "energy-constrained environments". — [Hazan, Greenberg, Ezra Tsur (2025)](https://exa.ai/library/publication/sch4yzkrwbv)
- Energy evidence from adjacent fields:
  - On-node TinyML filtering in acoustic WSNs cuts transmissions and extends node lifetime ([Roy et al., JTIT 2025](https://www.jtit.pl/jtit/article/view/2084)).
  - TinyChirp bioacoustics extended battery life from 2 weeks to 8 weeks with MCU-class models (RAM about 500 kB) ([arXiv 2407.21453 / IEEE IS2 2024](https://arxiv.org/html/2407.21453)).
  - B4W throwable acoustic intruder nodes lasted up to 170 days with 98.3% detection and 0.9% false alarms on dry leaves, using non-ML signal-energy features ([B4W, 2023](https://exa.ai/library/publication/sf805zm76c5)).
  - A self-powered TENG + accelerometer intruder sensor uses only STA/LTA thresholds, not ML ([Zhu et al. 2025](https://exa.ai/library/publication/2hdqj9ypn58)).
- TinyML-wide gaps (Heydari & Mahmoud, Sensors 2025, Sec. 5.3): "research gaps remain in areas such as scalability, standardization, model optimization, energy efficiency, and security". They call for "better benchmarking, including frameworks specific to TinyML" and for scaling "for large deployments involving thousands or millions of devices". — [MDPI](https://www.mdpi.com/1424-8220/25/10/3191)

#### P3 — Onboard perception on small UAVs (SWaP)

- **Habash, Abu Alqumsan, Zhou (Sensors 2025, 25(24):7563)**: improving small-object detection "generally comes with an increase in model complexity … making it increasingly difficult to satisfy the requirements for real-time applications on memory- and processing-constrained platforms". Fine-grained discrimination methods "increase computational burden … limiting their suitability for real-time onboard deployment". Some methods offer "real-time performance but not on edge device". — [MDPI](https://www.mdpi.com/1424-8220/25/24/7563)
- **Manzoor, Ahmad, Ahmad (2025 review; venue not verified)**: open challenges are "loss of fine-grained features at low resolutions, dataset imbalance, domain variability, and the trade-off between real-time processing and accuracy", plus the "absence of standardized benchmarks". Proposed future work: thermal-RGB fusion, NAS for UAV models, edge-cloud collaboration, self-supervised learning. — [entry](https://exa.ai/library/publication/cjf8vp24f99)
- **Thermal human detection on Jetson AGX Orin (Sensors 2025, PMC12733663)**: models trained on heterogeneous public thermal data "achieve poor results" in mountain terrain. YOLO "accuracy degrades significantly when testing specifically on a small object sub-dataset". — [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12733663/)
- **Military field evidence (CSIS)**: AI-enabled ATR "models require continuous, real-world data updates to maintain accuracy and adapt to evolving battlefield conditions", including against decoys and camouflage. This is a domain-shift and adversarial-adaptation problem. — [CSIS](https://www.csis.org/analysis/ukraines-future-vision-and-current-capabilities-waging-ai-enabled-autonomous-warfare)
- **Interceptor drones and autonomous turrets** are now a main counter to Shaheds and FPVs (Sky Sentinel AI turret; Terma–Odd Systems AI interceptors). All need onboard detection and tracking of a small aerial target under SWaP limits. — [CSIS, The New Salvo War](https://www.csis.org/index%2ephp/analysis/new-salvo-war); [NATO ACT](https://www.act.nato.int/article/innovation-challenge-fibre-optic-drones/) (AI-assisted autonomous turrets with "thermal optics, automatic tracking").

#### P4 — On-device threat and anomaly detection for UAVs (brief)

- **Mouatassim, El Guarmah, Airaj (2026 SLR, 110 articles 2019–2025)**: identified 53 UAV-relevant IDS datasets. Challenges include "the absence of standards and legal restrictions" on creating and sharing datasets. They propose 10 recommendations. — [entry](https://exa.ai/library/publication/0yt946p8wxm)
- **Graph-based CAN/UAVCAN IDS (arXiv 2412.02539)**: models can run on Cortex-M, unlike GPU-based IDS. However, "further work is required to optimize these systems for real-time deployment, particularly for UAVs with limited resources … test these systems in a real-time" setting. — [arXiv](https://arxiv.org/html/2412.02539)
- **UAVCAN ensemble IDS (Applied Sciences 2024, 14(13):5487)**: 97% detection, limited to 3 intrusion types. — [MDPI](https://www.mdpi.com/2076-3417/14/13/5487)
- **GNSS spoofing**:
  - Hardware-based detection needs costly extra sensors "not acceptable … in small UAVs".
  - ML models suffer "high rate[s] of false alarm and misdetection".
  - The best capsule net needs 123 MiB of memory and 0.5 s per prediction, which is not MCU-class.
  - [Int. J. Information Security 2025](https://link.springer.com/article/10.1007/s10207-024-00978-x)
  - The common spoofing dataset uses MATLAB-simulated attacks on real-flight GPS features. — [Sensors 2025, 25(13):4045](https://www.mdpi.com/1424-8220/25/13/4045)
- **UAVIDS-2025** (Zenodo; NS-3 simulated swarm, 122,171 flows, 5 classes) is simulation-only. — [Zenodo](https://zenodo.org/records/15336998)

### Inferences

**P1**
- Below the level of single-board computers, MCU or sub-watt real-time inference for drone detection is almost untested. Reviews list "edge deployment" as future work, and the best acoustic arrays still draw tens to 120 W.
- Fielded soldier-worn devices are RF-only. A passive, non-RF, wearable or vehicle-mounted detector for fiber-optic and autonomous-terminal FPVs is an unsolved, clearly defense-relevant application.
- Bird and distractor rejection is still weak in vision. Datasets often don't even label birds, so false-alarm rate (not mAP) is the operational bottleneck.

**P2**
- The open problem is not "can we classify footsteps". It is:
  - holding a low false-alarm rate over months on a fixed energy budget;
  - generalizing across terrain and soil;
  - handling overlapping events;
  - adding new threat classes (e.g. low-flying FPVs or a "sleeper" drone landing nearby) on the same node.

**P3**
- The gap is accuracy on tiny or thermal targets under onboard compute, plus robustness to fast-changing adversary countermeasures (decoys, camouflage, new vehicle types). Benchmark accuracy on public datasets does not transfer.

**P4**
- Datasets are mostly simulated, and few papers measure onboard latency, memory or energy on flight-controller-class hardware.

### Gaps
- I could not open the full text of Semenyuk et al. (IJCIP 2025), Kang et al. (AIP Advances 2025) Sec. VI or Altujar et al. (2025), so only abstract-level challenge items are quoted.
- I found no 2024–2026 peer-reviewed survey dedicated to edge, TinyML or low-power C-UAS. Edge deployment shows up only as "future direction" bullets inside general surveys.
- I found no peer-reviewed experimental paper on detecting fiber-optic FPVs specifically, whether by detecting the fiber spool or cable, or by acoustic or radar signatures. Only conceptual papers and a low-quality Academia.edu essay ([link](https://www.academia.edu/168307514/FIBER_OPTIC_DRONES_ARE_DETECTABLE_NOT_UNBREAKABLE)) exist.
- I found no academic source on detecting "sleeper" drones (landed or hibernating ambush drones). It is mentioned only in ISW.

---

## Q3. Measurable evaluation: which open datasets and benchmarks exist, and what is missing

### Takeaway
Benchmarks exist for vision and thermal (Anti-UAV410, CST Anti-UAV, Drone-vs-Bird, DUT Anti-UAV), event cameras (FRED, NeRDD), RF (DroneRF, DroneRFa, RFUAV), audio (DADS, DroneAudio) and multimodal setups (MMAUD).

Across them, the following are missing:
1. military FPV, fiber-optic or fixed-wing loitering munitions; most data are DJI consumer drones;
2. hardware-in-the-loop metrics (energy per inference, battery lifetime, latency on an MCU or NPU);
3. labeled distractors (birds, insects) and multi-drone scenes;
4. synchronized multimodal data captured by low-cost or wearable sensors;
5. long-duration always-on recordings with realistic false-alarm accounting.

For radar and seismic, public data are scarce, small or older.

### Cited Findings

**Vision, IR and event-camera datasets (P1)**
- **Anti-UAV410** (Huang et al., IEEE TPAMI 2024): thermal IR, 410 sequences, 438K boxes, 640×512. — Listed in [Dong et al. CVPRW 2025, Table 1](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf); challenge site [anti-uav.github.io](https://anti-uav.github.io/).
  - Missing: complex urban scenes and dynamic distractors; few tiny objects; incomplete frame-level attributes ([CST Anti-UAV](https://openaccess.thecvf.com/content/ICCV2025W/Findings/papers/Xie_CST_Anti-UAV_A_Thermal_Infrared_Benchmark_for_Tiny_UAV_Tracking_ICCVW_2025_paper.pdf)).
  - The 4th Anti-UAV Challenge (CVPR 2025) added multi-UAV tracking (up to 30 objects) with kites, balloons and birds as fake targets ([anti-uav.github.io](https://anti-uav.github.io/)).
- **CST Anti-UAV** (Xie et al., ICCV 2025 Workshops): thermal IR, 220 sequences, more than 240K boxes, 4.5× more tiny objects than earlier sets. It includes urban scenes, pedestrian, vehicle, bird and airplane distractors, and attributes such as thermal crossover. Release was described as "about to be publicly released". — [CVF PDF](https://openaccess.thecvf.com/content/ICCV2025W/Findings/papers/Xie_CST_Anti-UAV_A_Thermal_Infrared_Benchmark_for_Tiny_UAV_Tracking_ICCVW_2025_paper.pdf)
- **Anti-UAV (1st challenge, CVPR 2020)**: 318 RGB+IR videos (297K boxes). Only 4 DJI types; "most objects … are relatively large, and the backgrounds are clean". — [Coluccia et al. 2021](https://www.mdpi.com/1424-8220/21/8/2824); [CST Anti-UAV](https://openaccess.thecvf.com/content/ICCV2025W/Findings/papers/Xie_CST_Anti-UAV_A_Thermal_Infrared_Benchmark_for_Tiny_UAV_Tracking_ICCVW_2025_paper.pdf)
- **DUT Anti-UAV** (Zhao et al., IEEE T-ITS 2022): 10,000 images (10,109 boxes), more than 35 drone models, plus 20 tracking sequences, which is too few for training trackers. — [arXiv 2504.19347](https://arxiv.org/html/2504.19347); [CST Anti-UAV](https://openaccess.thecvf.com/content/ICCV2025W/Findings/papers/Xie_CST_Anti-UAV_A_Thermal_Infrared_Benchmark_for_Tiny_UAV_Tracking_ICCVW_2025_paper.pdf)
- **Drone-vs-Bird** (WOSDETC, since 2017; 8th edition at IJCNN 2025): RGB, 77 videos, 105K annotations (per Dong et al. Table 1). Birds are not annotated. The dataset grows each edition. Reviews: [Coluccia et al., Sensors 2021](https://www.mdpi.com/1424-8220/21/8/2824); ICASSP 2023 edition in IEEE OJSP 5:766–779 (2024), DOI 10.1109/OJSP.2024.3379073 ([cited in](https://exa.ai/library/publication/r45j7rqhssh)).
- **FRED** (Magrini et al., 2025, arXiv 2506.05163): RGB + event camera at 1280×720, more than 7 h per modality, 5 drone models (mini to commercial), rain, low light, insects. Tasks: detection, tracking, trajectory forecasting. Self-described as "the largest existing drone detection dataset". — [arXiv](https://arxiv.org/pdf/2506.05163v1.pdf); [project page](https://miccunifi.github.io/FRED/)
- **NeRDD** (Magrini et al., 2024): event + RGB, 3.5 h, 115 videos. — [arXiv 2409.16099](https://arxiv.org/html/2409.16099v1)
- **F-UAV-D** (Mandula et al., I2MTC 2024): event + RGB, 0.5 h, Jetson Xavier NX setup. — [cited in NeRDD](https://arxiv.org/html/2409.16099v1)
- **EventUAV** (ICMR 2026): 87 event clips at 5–100 m. — [ACM DL](https://dl.acm.org/doi/10.1145/3805622.3810721)
- **Halmstad Drone dataset** (Svanström et al.): RGB, IR and audio; 650 videos and 90 audio clips (per AIP Advances Table II "650 videos and 90 audios"). — [Kang et al. AIP Advances 2025](https://pubs.aip.org/aip/adv/article/15/12/120701/3373725/From-classical-approaches-to-recent-advancements-A); [Dong et al.](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf)

**Multimodal (P1)**
- **MMAUD** (Yuan et al., ICRA 2024, DOI 10.1109/ICRA57147.2024.10610957): stereo vision, 2 LiDARs, mmWave radar and 4 audio array nodes, with Leica millimetre ground truth.
  - About 1,700 s in V1. Drones: Mavic2, Mavic3, Avata, Phantom4, M300.
  - V2/V3 (CVPR UG2+ 2024 challenge) go up to 100 m and are "designed for actual warfare simulation".
  - No RF modality.
  - Audio 3D position error is 2.6 m because of machinery noise.
  - The mmWave radar costs about $3,700.
  - [ar5iv](https://ar5iv.labs.arxiv.org/html/2402.03706); [GitHub](https://github.com/ntu-aris/MMAUD); [site](https://ntu-aris.github.io/MMAUD/)

**RF (P1)**
- **RFUAV** (2025, arXiv 2503.09033): about 1.3 TB raw IQ from 37 UAVs (USRP), SNR tools (−20 to 20 dB), with open baseline and evaluation tools. Mostly DJI, including DJI FPV and Avata 2. — [arXiv](https://arxiv.org/html/2503.09033); [GitHub](https://github.com/kitoweeknd/RFUAV/)
- **DroneRFa** (Yu et al., J. Electronics & Information Technology 46(4), 2024, DOI 10.11999/JEIT230570): about 25 drone types, no precise per-packet SNR. — [cited in RFUAV](https://arxiv.org/html/2503.09033)
- **DroneRF** (Al-Sa'd / Allahham et al., 2019): 3 drones only. — [cited in RFUAV](https://arxiv.org/html/2503.09033); [Dong et al.](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf)
- **CardRF**: an outdoor UAV / Bluetooth / Wi-Fi RF dataset (Medaiyese et al., about 2022). I did not retrieve details in this session (see Gaps).

**Acoustic (P1, P2)**
- **DADS — Drone Audio Detection Samples** (Hugging Face, uploader geronimobasso; MIT license; about 2024–2025):
  - 180,320 files, 6.81 GB, 16 kHz mono.
  - Drone class: 163,591 files, 27.1 h, average 0.6 s per clip. No-drone class: 16,729 files, 33.8 h.
  - It aggregates earlier sets (e.g. Al-Emadi DroneAudioDataset 2019; Yi et al. 2023 Zenodo).
  - Self-described as the "largest publicly available drone audio database".
  - Missing: no drone-type, range or SNR labels; binary only; mostly consumer drones; very short drone clips.
  - [HF](https://huggingface.co/datasets/geronimobasso/drone-audio-detection-samples)
- **DroneAudio** (Al-Emadi et al., 2019): CNN accuracy 96.38% (2-class) and 92.94% (3-class). — [Dong et al.](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf)
- **Other acoustic sets** (AIP Advances 2025, Table II): 4,924 files / 23.42 h (44 drone samples); 1,300 Bebop/Mambo files; a distance series every 5 m from 5 to 50 m; 17 UAV variants at 8 m altitude; a localization set of 33,090 s / 31.95 GB at 96 kHz. — [Kang et al.](https://pubs.aip.org/aip/adv/article/15/12/120701/3373725/From-classical-approaches-to-recent-advancements-A)

**Radar micro-Doppler (P1)**
- **Karlsson (Zenodo 2021, DOI 10.5281/zenodo.5511912)**: 77 GHz FMCW (SAAB SIRS 1600). 6 drones including a custom FPV, birds (seagull, gulls, heron, pigeon, raven) and humans; 1.5 GB; CC-BY. — [Zenodo](https://zenodo.org/records/5511912)
- **DIAT-mSAT** (DRDO): 6 classes, 4,849 micro-Doppler samples (drone, bird, RC plane, rotors). Reported through a SIH 2024 GitHub project, so this is a secondary source. — [GitHub](https://github.com/Incharajayaram/Micro-Classify)
- **LSS-FMCWR-2.0** (Chen et al., 2025): K-band and L-band, multi-angle, 5 rotorcraft plus bird models. — [entry](https://exa.ai/library/publication/xbms8cydhz5)
- **Chen et al. (Remote Sensing 2022)**: K-band; 5 drones plus bionic and seagull birds; 4,320 / 1,080 / 240 samples. Real bird data are limited. — [MDPI PDF](https://mdpi-res.com/d_attachment/remotesensing/remotesensing-14-01107/article_deploy/remotesensing-14-01107-v2.pdf?version=1646039697)
- Several radar bird/drone datasets are explicitly non-public. — [Tsang et al., Signals 2023](https://www.mdpi.com/2624-6120/4/2/18)

**Seismic and acoustic UGS (P2)**
- **ACIDS** (acoustic-seismic ID dataset): 9 ground-vehicle types, more than 270 runs, 3 environments, 1,025 Hz, CPA 25–100 m. It includes cross-condition domain shift (speed, distance, terrain). This is an older Army dataset. — [described in NeurIPS 2023 FOCAL supplement](https://papers.nips.cc/paper_files/paper/2023/file/93e98ddf39a9beb0a97fbbe56a986c80-Supplemental-Conference.pdf)
- **MOD**: RaspberryShake geophone plus mic array; 7 targets including a human and a UGV; 2 sites. Planned for release. — [same](https://papers.nips.cc/paper_files/paper/2023/file/93e98ddf39a9beb0a97fbbe56a986c80-Supplemental-Conference.pdf)
- **M3N-VC**: geophone (200 Hz) plus mic (1.6 kHz); 6 scenes; 6–8 GPS-synced nodes per scene; 4 civilian cars. — [GitHub](https://github.com/restoreml/m3n-vc)
- **ASD — Acoustic and Seismic Dataset for Mobile Target Recognition** (IEEE DataPort): 17,395 s; environment, human and vehicle classes; soft and hard ground; highway and train noise. — [IEEE DataPort](https://ieee-dataport.org/documents/acoustic-and-seismic-dataset-mobile-target-recognition)
- **HyMAD border dataset** (CSIR-CMERI geophones, 6 sensors over 100 m, 8 kHz): 4,000 samples per class, multi-activity created by superposition. Public availability is not stated. — [arXiv 2511.14698](https://arxiv.org/html/2511.14698)

**UAV IDS / GNSS (P4)**
- 53 UAV-relevant IDS datasets (2019–2025). — [Mouatassim et al. 2026](https://exa.ai/library/publication/0yt946p8wxm)
- **UAVIDS-2025**: NS-3 simulated swarm traffic. — [Zenodo](https://zenodo.org/records/15336998)
- **Multi-channel GPS spoofing dataset**: 8-channel USRP plus GNSS-SDR on a real UAV; 13 features; 3 MATLAB-simulated attack levels. — [Sensors 2025](https://www.mdpi.com/1424-8220/25/13/4045)

**Evaluation practice gap**
- Most papers report accuracy or mAP on GPU. Edge papers report FPS on Jetson-class devices. Examples:
  - YOLO11-AU-IR keeps 95% mAP50 under INT8 CPU-only inference on a Jetson TX2 ([PLOS One 2025](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0330074));
  - a thermal human-detection study measured energy on a Jetson AGX Orin ([PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12733663/)).
- A real-time defense threshold is cited as "detection accuracy above 90% and latency below 200 ms" (Kandeepan et al., as cited by [Ghouli, Acta Acustica 2026](https://acta-acustica.edpsciences.org/articles/aacus/full_html/2026/01/aacus250134/aacus250134.html)).

### Inferences
Concretely missing evaluation assets that a thesis could address in a small way:

**P1**
- An open recording set of FPV-class racing quads (5–7 inch, high-RPM, often analog VTx). Fiber-optic variants ideally, or at least the same airframe with the radio off.
- The set should have synchronized low-cost sensors (MEMS mic array, small thermal camera, event camera or 24/60 GHz radar) and range, bird and wind labels.
- No dataset I found contains fiber-optic FPVs.

**P1/P2**
- Benchmarks that report energy per inference, false alarms per hour and node lifetime alongside accuracy. No drone or UGS benchmark I found reports these jointly.

**P2**
- Public seismic sets are civilian vehicles or older Army sets. No public set covers crawling or slow-walking intruders, tracked military vehicles, or overlapping events recorded in the field.

**P3**
- Public UAV-view thermal sets are not military-target, camouflage or decoy oriented. CSIS says ATR models need continual real-world updates, so on-device adaptation or rapid retraining is untested on public benchmarks.

**Radar**
- Few open low-cost FMCW micro-Doppler sets include FPV drones. The Karlsson 77 GHz set has one custom FPV, but uses a high-end SAAB radar.

### Gaps
- CardRF: I did not retrieve exact size, number of UAVs or controllers, or the venue in this session.
- I could not verify sizes or years for VisDrone, HIT-UAV, BIRDSAI, DroneVehicle or Det-Fly in this session. They are commonly used UAV-view or anti-UAV sets. Check them before citing.
- I could not confirm whether FRED, NeRDD or CST Anti-UAV have since appeared in peer-reviewed journals; I treat them as preprint or workshop.
- I found no open dataset or benchmark with recordings of fiber-optic FPVs or of a deployed fiber cable or spool.

---

## Q4. Which gaps are realistically addressable in a 12–16 month MSc with a hardware prototype

### Takeaway
The most feasible gaps combine three things: a cheap passive sensor, a public dataset for pre-training, and a small self-recorded field set with energy and false-alarm metrics.

Feasible areas:
- low-power acoustic (and optionally seismic or event-camera) detection on MCU or NPU nodes;
- non-RF wearable or vehicle detection of FPV-class drones, measured at short range;
- bird- and distractor-aware rejection for edge vision or thermal;
- always-on wake-up hierarchies for UGS;
- small onboard IDS or GNSS-anomaly monitors on flight-controller-class hardware.

Long-range radar, true fiber-optic FPV field trials and military-target ATR datasets are generally beyond an MSc. The reasons are access, regulation and classification limits.

### Cited Findings

**Low-cost hardware baselines exist**
- Acoustic: MEMS mics (INMP441, I²S) are "ideal for real-time embedded systems" ([Ghouli 2026](https://acta-acustica.edpsciences.org/articles/aacus/full_html/2026/01/aacus250134/aacus250134.html)). Sky Fortress nodes cost $300–500 ([FlightGlobal](https://www.flightglobal.com/military-uavs/2024/09/how-ukraine-turned-mobile-phone-microphones-into-an-air-defence-network/)).
- Array size: 11 or more mic sub-arrays match 32-mic performance, and a helmet-scale aperture was proposed but not built ([Blass & Graf 2025](https://dael.euracoustics.org/confs/fa2025/data/articles/000269.pdf)).
- Event camera on Jetson Xavier NX ([Mandula et al. 2024, via FRED](https://arxiv.org/pdf/2506.05163v1.pdf)).
- 24 GHz FMCW module ranges are only tens of metres for small drones ([Maya et al. 2025](https://www.researchgate.net/publication/393741936_Evaluation_of_Additive_Manufacturing_Techniques_to_Increase_Drone_Radar_Detection_Range)).

**Public pre-training data exist**
- Audio: DADS, 60.9 h ([HF](https://huggingface.co/datasets/geronimobasso/drone-audio-detection-samples)).
- Event: FRED, 7 h ([arXiv](https://arxiv.org/pdf/2506.05163v1.pdf)).
- IR: Anti-UAV410 ([anti-uav.github.io](https://anti-uav.github.io/)).
- RF: RFUAV, 37 UAVs ([arXiv](https://arxiv.org/html/2503.09033)).
- Radar: Karlsson 77 GHz ([Zenodo](https://zenodo.org/records/5511912)).
- Seismic/acoustic: ACIDS, M3N-VC, ASD ([NeurIPS suppl.](https://papers.nips.cc/paper_files/paper/2023/file/93e98ddf39a9beb0a97fbbe56a986c80-Supplemental-Conference.pdf); [GitHub](https://github.com/restoreml/m3n-vc); [IEEE DataPort](https://ieee-dataport.org/documents/acoustic-and-seismic-dataset-mobile-target-recognition)).

**Explicitly stated open items that fit an MSc**
- "Few studies address power constraints and real-time requirements … multiple drones, identification of drone types, and 3D localization remain open problems." — [Ghouli 2026](https://acta-acustica.edpsciences.org/articles/aacus/full_html/2026/01/aacus250134/aacus250134.html)
- Need for "lightweight and efficient algorithms that can operate on edge devices" and for "distributed and collaborative detection systems". — [Mrabet et al. 2024](https://www.frontiersin.org/journals/communications-and-networks/articles/10.3389/frcmn.2024.1440727/full)
- Birds unlabeled, so false alarms in flocks. — [Coluccia et al. 2021](https://www.mdpi.com/1424-8220/21/8/2824)
- IR "trilemma" of small-target accuracy, real-time speed and edge deployment. — [PLOS One 2025](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0330074)
- Overlapping seismic activities. — [HyMAD](https://arxiv.org/html/2511.14698)
- TinyML benchmarking and energy-efficiency gaps. — [Heydari & Mahmoud 2025](https://www.mdpi.com/1424-8220/25/10/3191)
- Real-time IDS on resource-limited UAVs still untested. — [arXiv 2412.02539](https://arxiv.org/html/2412.02539)

**NATO's own requirement set gives measurable targets**
- 500 m detection, day and night, adverse weather, under 100 kg, low cost ([NATO ACT](https://www.act.nato.int/article/innovation-challenge-fibre-optic-drones/)).
- Fielded wearable baseline: about 1.1 kg, 10–14 h battery ([MyDefence](https://mydefence.com/wearable-solutions/wingman-drone-detector/)).

### Inferences
Feasibility ranking. This is my judgement; it suggests no specific topics, only how addressable each gap is.

1. **High feasibility: P1 acoustic / non-RF FPV detection on a low-power node (MCU or small NPU), wearable or vehicle-mounted.**
   - Inputs: public data (DADS) plus own recordings of a legal FPV-class quad with the radio link off (a stand-in for RF-silent flight).
   - Measurable outputs: Pd/Pfa vs range, false alarms per hour under wind and walking noise, mW and battery hours, latency.
   - Directly maps to the stated gaps: power constraints, wearable arrays, RF-silent threats.
   - Risks: flight permits; true fiber-optic FPV access is unlikely.
2. **High feasibility: P2 always-on UGS node with a hierarchical wake-up (threshold, then tiny model, then radio).**
   - Measurable: lifetime model plus field false alarms over days, cross-site generalization (2–3 soils), overlapping events.
   - Public seismic and acoustic sets exist for pre-training.
   - The "drone overhead" class can be added as a cross-over with P1.
3. **Medium feasibility: bird and distractor-aware edge vision, thermal or event detection.** Public data exist (Drone-vs-Bird, Anti-UAV410, FRED), and running on a Jetson- or NPU-class board is doable. Novelty would come from distractor labeling, a false-alarm-focused metric, or an energy-accuracy trade-off. Thermal cameras with useful resolution add cost.
4. **Medium feasibility: P3 onboard small-object or thermal detection on a small UAV companion computer.**
   - Feasible on public UAV-view sets plus own flights.
   - Military-target realism (camouflage, decoys) and adversarial adaptation are hard to reach without restricted data.
5. **Medium feasibility, narrow scope: P4 onboard IDS or GNSS-interference monitor on an MCU or flight controller**, using existing datasets (UAVCAN attack logs, the GPS-features dataset) and measuring latency and memory on real hardware. Overlaps with the other researcher's GNSS scope.
6. **Low feasibility within 12–16 months:** long-range radar micro-Doppler systems (hardware cost, about $3,700 for the MMAUD radar alone; needs low phase noise); field trials with real fiber-optic FPVs; swarm-scale C-UAS fusion; military ATR datasets.

### Gaps
- I found no source that sizes typical MSc-scale prototypes in this domain beyond the examples above (Mays 2024 thesis; Ghouli 2026; B4W).
- Turkish legal constraints on drone flights and RF recording were not researched.

### Source register (bibliographic details; quartiles from general knowledge, SJR unverified unless stated)

**Peer-reviewed surveys and reviews (2024–2026)**

| # | Authors | Title | Venue / year | DOI or URL | Quartile |
|---|---|---|---|---|---|
| 1 | Dong Y., Wu F., Zhang S., Chen G., Hu Y., Yano M., Sun J., Huang S., Liu F., Dai Q., Cheng Z.-Q. | Securing the Skies: A Comprehensive Survey on Anti-UAV Methods, Benchmarking, and Future Directions | CVPR 2025 Workshops (Anti-UAV) | [CVF](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf) | Conference workshop, no quartile |
| 2 | Mrabet M., Sliti M., Ben Ammar L. | Machine learning algorithms applied for drone detection and classification: benefits and challenges | Frontiers in Communications and Networks, 2024 | 10.3389/frcmn.2024.1440727 | Unverified (likely Q2–Q3) |
| 3 | Seidaliyeva U. et al. | Advances and Challenges in Drone Detection and Classification Techniques: A State-of-the-Art Review | Sensors 24(1):125, 2024 | 10.3390/s24010125 | Q1/Q2 by category, SJR unverified. First author's name is from memory; the snippet showed no authors. |
| 4 | Rahman M.H. et al. | A Comprehensive Survey of UAV Detection and Classification Using ML Approach: Challenges, Solutions, and Future Directions | Remote Sensing 16(5):879, 2024 | 10.3390/rs16050879 | Q1, SJR unverified. Author list from memory; the snippet showed no authors. |
| 5 | Semenyuk V., Kurmashev I., Lupidi A., Alyoshin D., Kurmasheva L., Cantelli-Forti A. | Advances in UAV detection: integrating multi-sensor systems and AI for enhanced accuracy and efficiency | Int. J. Critical Infrastructure Protection 49, 2025 | 10.1016/j.ijcip.2025.100744 | Q1, SJR unverified |
| 6 | Kang C., Huang Q., Sun F., Liang X., Xu L. | From classical approaches to recent advancements: A holistic review of acoustic detection for UAVs | AIP Advances 15(12):120701, 2025 | [AIP](https://pubs.aip.org/aip/adv/article/15/12/120701/3373725/From-classical-approaches-to-recent-advancements-A) | Q2, SJR unverified |
| 7 | Altujar H., Abdul Gaffoor A.R., Sameer R., Faisal M., Butt F.A. | A Review of Acoustic Techniques for Drone Detection | 2025 | [entry](https://exa.ai/library/publication/37xcx9hkxdf) | Venue unverified |
| 8 | Habash N., Abu Alqumsan A., Zhou T. | Recent Real-Time Aerial Object Detection Approaches, Performance, Optimization, and Efficient Design Trends for Onboard Performance: A Survey | Sensors 25(24):7563, 2025 | 10.3390/s25247563 | Q1/Q2, SJR unverified |
| 9 | Manzoor S., Ahmad F., Ahmad M. | Advances and Open Challenges in Small Object Detection for UAV Imagery: A Deep Learning Perspective | 2025 | [entry](https://exa.ai/library/publication/cjf8vp24f99) | Venue unverified |
| 10 | Heydari S., Mahmoud Q.H. | Tiny Machine Learning and On-Device Inference: A Survey of Applications, Challenges, and Future Directions | Sensors 25(10):3191, 2025 | 10.3390/s25103191 | Q1/Q2, SJR unverified |
| 11 | Mouatassim T., El Guarmah E.M., Airaj M. | A comprehensive literature review on intrusion detection datasets for UAVs | 2026 | [entry](https://exa.ai/library/publication/0yt946p8wxm) | Venue unverified |
| 12 | Metalidi O., Belyakov R., Kovalchuk O.S. | Analysis of methods for detecting UAVs using wireless sensor networks | Ukrainian journal, 2026 | [entry](https://exa.ai/library/publication/qd3q7bhzw45) | Not indexed / unverified |

Also cited in the notes, for reference: Alzubaidi, IEEE Access 13 (2025), 10.1109/ACCESS.2025.3552329; Ogab et al., IEEE Access 13 (2025), 10.1109/ACCESS.2025.3575236. Both are SLRs on UAV and IoD IDS, listed in [11]; I did not read them.

**Dataset and benchmark papers**
- Coluccia A. et al., "Drone vs. Bird Detection: Deep Learning Algorithms and Results from a Grand Challenge". Sensors 21(8):2824, 2021, DOI 10.3390/s21082824. 2024 OJSP edition: DOI 10.1109/OJSP.2024.3379073. IJCNN 2025 edition: [entry](https://exa.ai/library/publication/r45j7rqhssh).
- Huang B. et al., "Anti-UAV410". IEEE TPAMI 2024 (Q1). Authors from memory, unverified; listed in [Dong et al.](https://openaccess.thecvf.com/content/CVPR2025W/Anti-UAV/papers/Dong_Securing_the_Skies_A_Comprehensive_Survey_on_Anti-UAV_Methods_Benchmarking_CVPRW_2025_paper.pdf).
- Xie B., Zhang C., Wang F., Liu P., Lu F., Chen Z., Hu W., "CST Anti-UAV". ICCV 2025 Workshops.
- Yuan S. et al., "MMAUD". ICRA 2024, DOI 10.1109/ICRA57147.2024.10610957.
- Magrini G. et al., "FRED: The Florence RGB-Event Drone Dataset". arXiv 2506.05163, 2025.
- Magrini G. et al., "NeRDD", arXiv 2409.16099, 2024. Mandula J. et al., I2MTC 2024, DOI 10.1109/I2MTC60896.2024.10561168.
- "RFUAV: A Benchmark Dataset for UAV Detection and Identification". arXiv 2503.09033, 2025; [GitHub](https://github.com/kitoweeknd/RFUAV/).
- Yu N. et al., "DroneRFa". JEIT 46(4), 2024, DOI 10.11999/JEIT230570.
- DADS (Hugging Face, [link](https://huggingface.co/datasets/geronimobasso/drone-audio-detection-samples)).
- Karlsson A., 77 GHz radar dataset, Zenodo 10.5281/zenodo.5511912 (2021).
- Chen X. et al., Remote Sensing 14:1107 (2022).
- Chen X. et al., LSS-FMCWR-2.0 (2025).
- UAVIDS-2025 (Zeng Q., Bashir A., Nait-Abdesselam F.; Zenodo 15336998).

**Experimental papers**
- Ghouli Z., Acta Acustica 2026 (Q2, SJR unverified).
- Blass M., Graf F., Forum Acusticum 2025.
- Chen Y. et al., PLOS One 2025, DOI 10.1371/journal.pone.0330074 (Q1 multidisciplinary, SJR unverified).
- HyMAD, arXiv 2511.14698.
- Hazan A., Greenberg S., Ezra Tsur E. (2025).
- Roy B.B., Das S., Mondal U.K., JTIT 2025.
- Huang Z. et al., TinyChirp, IEEE IS2 2024, DOI 10.1109/IS262782.2024.10704131.
- Graph CAN IDS, arXiv 2412.02539.
- Applied Sciences 14(13):5487 (2024).
- Sensors 25(13):4045 (2025).
- Int. J. Information Security (2025), DOI 10.1007/s10207-024-00978-x.

**Defense analysis (field relevance only)**
- RUSI Feb 2025 special report.
- CSIS: Ukraine AI-enabled autonomous warfare; The New Salvo War; Drone Saturation; The Russia-Ukraine Drone War.
- ISW, Aug 2025 special report.
- NATO ACT, 16th Innovation Challenge (Jun 2025).
- US Army CALL No. 26-1115, "Listening to the Sky" (Mar 2026).
- Defense One (Jul 2024); FlightGlobal (Sep 2024).
