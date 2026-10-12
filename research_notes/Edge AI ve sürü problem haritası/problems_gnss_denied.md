# Open application problems: UAV / UAV-swarm navigation and positioning under GNSS denial and electronic warfare (2024-2026)

Scope note: these notes are input for choosing a problem area. They map the problem and where current solutions fall short. They do not propose thesis topics. Research date: 2026-10-12.

Source-quality legend: [J] peer-reviewed journal, [C] conference, [P] preprint (arXiv/Preprints.org), [G] government/regulator document, [N] news/trade press/vendor. Scimago quartiles are marked "unverified" unless checked in this session. None were checked directly against scimagojr.com because several publisher domains failed DNS resolution from this environment.

Core reference set (cited throughout):
- **Zeng, Lu, Zhao, Xiao, Ni, Han, Li**, "GNSS Jamming and Spoofing Threats in UAV Navigation: Countermeasure Status and Challenges", *IEEE Communications Surveys & Tutorials*, 2026, DOI 10.1109/COMST.2026.3680438 [J; COMST is generally Q1, unverified here]. Author PDF: https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf
- **Jarraya, Al-Batati, Kadri, Abdelkader, Ammar, Boulila, Koubaa**, "GNSS-denied unmanned aerial vehicle navigation: analyzing computational complexity, sensor fusion, and localization methodologies", *Satellite Navigation*, 2025, DOI 10.1186/s43020-025-00162-z [J; quartile unverified]. Reviews 132 papers. https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z
- **Couturier & Akhloufi**, "A Review on Deep Learning for UAV Absolute Visual Localization", *Drones* 8(11):622, 2024, DOI 10.3390/drones8110622 [J; quartile unverified]. https://www.mdpi.com/2504-446X/8/11/622/htm
- **Radoš, Brkić, Begušić**, "Recent Advances on Jamming and Spoofing Detection in GNSS", *Sensors* 24(13):4210, 2024, DOI 10.3390/s24134210 [J; quartile unverified]. https://www.mdpi.com/1424-8220/24/13/4210
- **Tymofieiev & Rogovyi**, "Sensor modalities for relative localization of cooperative UAV swarms in GNSS-denied environments", *Bulletin of NTU "KhPI"*, issue 2(11) 2025 (online Jan 2026), DOI 10.20998/2413-3000.2025.11.8 [J, low-tier national journal, likely not Q1-Q2]. https://pm.khpi.edu.ua/article/view/350033

---

## Q1. Why GNSS-denied / contested navigation matters now (field evidence, defense relevance)

### Takeaway
Since 2022, GNSS interference has gone from a niche risk to a measured, routine condition in several regions (Baltic, Eastern Mediterranean/Middle East, Black Sea, Ukraine front). Spoofing is growing faster than jamming. In Ukraine, jamming is a primary cause of drone loss, and both sides are moving to GNSS-independent (vision/terrain-based) navigation. The defense pull is direct and current.

### Cited Findings
**Civil-aviation scale (best proxy for regional EW intensity)**
- A joint submission to ICAO by Sweden and five neighbouring states reports that nearly **123,000 flights** were affected by interference traced to Russian territory in the **first four months of 2025**, over Poland, the Baltic states, Finland and Sweden. This is a secondary report of a government submission; I did not open the primary ICAO working paper. — [defencematters.eu summary](https://defencematters.eu/?p=2384); [ICAO APAC 2025 symposium deck on GNSS vulnerabilities](https://www.icao.int/sites/default/files/APAC/Meetings/2025/2025%20ICAO%20APAC%20Radio%20Navigation%20Symposium%20%20Radio%20N/4-Setting%20the%20Scene/SP03-ICAO-APAC-GNSS-Vulnerabilities-Threats.pdf)
- OPSGROUP's 2024 workgroup tracked spoofing rising from **~300 affected flights/day in early 2024 to ~1,500/day by August 2024**, and **41,000 flights affected in a single month** of 2024. In an OPSGROUP survey of ~2,000 crew, close to **70%** rated spoofing's safety impact "very high or extreme". [N, secondary] — [Jeppesen, "Flight Deck in Focus: Managing GPS Interference during Enroute Operations", 5 Aug 2026](https://news.jeppesen.com/?p=2611)
- IATA's 2025 Safety Report (as cited by Jeppesen) gives a **+67% increase in reported jamming** and a **+193% increase in reported spoofing between 2023 and 2025**. [N, secondary; primary IATA report not opened] — [Jeppesen](https://news.jeppesen.com/?p=2611)
- Another secondary source cites IATA data showing "GPS signal loss" incidents up **220% between 2021 and 2024**, alongside the EASA-IATA joint plan from the Cologne workshop of 22-23 May 2025. Unverified against IATA primary data. — [aviacionaldia.com](https://aviacionaldia.com/en/2025/06/easa-and-iata-launch-global-plan-to-mitigate-gnss-interference-risks.html)
- Zeng et al. (IEEE COMST 2026) cite **>1,600 GNSS interference instances reported by civil aviation in the Baltic region in H1 2024**. The ~1,600 count and the ~123,000-flight figure measure different things (reports vs affected flights). — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- EASA SIB 2022-02 was first published March 2022. Rev. 3 is dated 5 July 2024 and **Rev. 4 3 July 2026**; Rev. 4 builds on a joint EASA-EUROCONTROL task force. EASA states that interference has increased since February 2022 in "severity of its impact" and "intensity and sophistication", affecting areas around conflict zones, the Black Sea, Middle East, Baltic Sea and Arctic. [G] — [EASA news](https://www.easa.europa.eu/en/newsroom-and-events/news/easa-updates-safety-information-bulletin-gnss-interference); [EASA SIB 2022-02R2 PDF](https://www.copac.es/wp-content/uploads/2023/11/EASA_SIB_2022-02R2_1.pdf)
- EASA's monitoring page reportedly combines aircraft reports with ADS-B data to rank affected FIRs. A 15 July 2026 ranking reportedly included Ankara, Istanbul, Warsaw, Tallinn, Riga, Helsinki and Vilnius. [secondary; EASA page not opened] — [geoawesome](https://geoawesome.com/easa-updates-gnss-guidance-as-jamming-and-spoofing-surge-what-geospatial-professionals-need-to-know/)

**Physics of the threat (why small UAVs are easy targets)**
- A **1 W jammer can disrupt GNSS reception within ~30 km**. Under strong jamming, a u-blox 5H receiver at JSR 65 dB and 70 dB achieved valid positioning only **16% and 14%** of the time. — [Zeng et al. 2026, COMST](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- Reported spoofing attacks on vehicles achieve controlled position errors (3D spoofing error better than 1.01 m in one cited work; 157.27 m pull-off in 100 s in another). Scenario-constrained dynamic spoofing raised the success rate from <40% to ~75% (Chang et al.). — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- Low-cost SDRs (HackRF, LimeSDR) put jamming and spoofing within wide reach. — [Radoš et al., Sensors 2024](https://www.mdpi.com/1424-8220/24/13/4210)

**Ukraine (defense relevance)**
- IEEE Spectrum (published 2 June 2025) reports "tens of thousands of jammers" along the front lines. It cites a RUSI estimate that Ukraine may be losing **~10,000 drones/month, mostly to jamming**. It also covers neural-network optical navigation (e.g., KrattWorks Ghost Dragon) as the response to jamming and spoofing. [N; figures quoted via search snippet; full article text not retrievable] — [IEEE Spectrum](https://spectrum.ieee.org/ukraine-killer-drones)
- Ukrainian special-forces software "Eagle Eyes" (per The Economist via Unmanned Airspace) compares live downward video with an onboard map stitched from prior reconnaissance imagery. It reportedly lets drones keep flying after being jammed and is "cheap enough for kamikaze drones". [N, secondhand] — [Unmanned Airspace](https://www.unmannedairspace.info/?p=28136)
- Without GNSS, operators manually compare camera feed with satellite maps and landmarks. Flat, uniform terrain in eastern Ukraine makes this harder. A Ukrainian colonel reported **nearly 100 drones lost to GPS spoofing**. [N, Business Insider reprint] — [lucorg/Business Insider reprint](https://lucorg.com/?p=19076)

### Inferences
- The operational problem has shifted from "GNSS loss" (jamming, detectable) to "GNSS lies" (spoofing, which needs detection plus integrity). This is why integrity monitoring (Q2-D) is as important as alternative positioning.
- The Ukraine evidence points to downward-camera map matching as the fielded workaround. The documented weak spots (flat/uniform terrain, cheap compute) line up with gaps the academic surveys list (Q2-B).
- Turkey-relevant context: Ankara and Istanbul FIRs reportedly appear in EASA's mid-2026 affected-FIR ranking (secondary source). This could matter for a Turkish thesis's motivation section but should be verified on EASA's page.

### Gaps
- Primary IATA 2025 Safety Report figures and the primary ICAO working paper (Sweden + 5 states) were not opened. Numbers above are secondary.
- The OPSGROUP primary "GPS Spoofing Workgroup" report was not accessed. No 2025-2026 OPSGROUP daily-flight figures were found.
- No authoritative, quantitative public data was found on UAV-specific (rather than airliner) GNSS interference incidence.

---

## Q2. Current solutions and where they fall short (per sub-problem, from 2024-2026 survey "challenges/future directions" sections)

### Takeaway
Every sub-area has the same three gaps: (1) methods trained or validated on simulated or narrow data do not generalize to real EW environments; (2) the methods that work best (deep matching, array antennas, collaborative SLAM) exceed small-UAV SWaP, and embedded, real-time validation is rare; (3) components are studied in isolation (detection vs mitigation, jamming vs spoofing, absolute vs relative positioning, single UAV vs swarm), and integrity (knowing when the estimate is wrong) is largely missing.

### Cited Findings

#### A. GNSS jamming/spoofing detection and mitigation onboard small UAVs
- **Current methods** fall into three families: signal processing, array antennas (CRPA), and AI-based methods. — [Zeng et al., IEEE COMST 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- **Reported ML detection performance** (as tabulated by Zeng et al.): MLP jamming detection 98.9% DA / 0.28% FAR; sliding-window pre-detection on u-blox M8T 99.97% DA; TCN-Transformer federated learning 91.97% DA / F1 91%; autoencoder spoofing detection 99.53% DA, 1% FAR, 0.39 s inference; XGBoost 95.25% DA / 4.3% FAR; PCA-CNN-LSTM 99.43% DA; AdaBoost-CNN 95.83% on only 120 measured samples. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
  - Note: these near-99% numbers mostly come from in-distribution test splits of the same dataset. The same survey says performance degrades out of distribution (next bullet).
- **Zeng et al. 2026, Sec. VI "Challenges"** (close paraphrase):
  - *VI-A "Technical Bottlenecks Under Onboard Resource Constraints"*: payload, compute and power limits block multi-element arrays and deep-learning signal reconstruction. CNN/RNN/Transformer models have high latency and memory cost and often need dedicated accelerators.
  - *VI-B "Insufficient Flexibility of Existing Countermeasures"*: cascaded "detect-then-suppress" chains add latency. Techniques are narrow (e.g., time-frequency filtering handles narrowband but not broadband jamming). AI methods depend on training-data coverage, degrade when real interference falls outside the training distribution, and use offline training, which limits real-time adaptation.
  - *VI-C "Deficient UAV-Specific Strategies"*: methods are either generic multisensor fusion (limited by IMU drift or visibility) or signal-level only. Most handle jamming **or** spoofing, not both, and do not exploit UAV flight-manoeuvre characteristics.
  - *VI-D "Emerging Challenges in UAV Swarm-Based Anti-Interference"*: real-time fusion and distributed decision-making add latency; inter-drone links are themselves vulnerable; compromised nodes reduce redundancy.
- **Zeng et al. 2026, Sec. VII "Future Directions"**: (A) low-cost compact arrays (e.g., using dual-antenna RTK hardware), multi-frequency/multi-constellation redundancy, LEO augmentation; (B) unified end-to-end detection-mitigation, larger datasets, lightweight networks (pruned or attention transformers, knowledge distillation); (C) GNSS-centric multisource deep fusion, swarm collaborative countermeasures via distributed/federated learning, and DRL + transfer learning for closed-loop "perception-decision" response. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- **CRPA constraint**: suppression capability scales with the number of array elements, but each element adds cost, weight, power and compute. UAV payload limits element count and therefore gain and directivity. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- **Radoš et al., Sensors 2024, Conclusions** (quotes): "One of the future directions and challenges ... should be research and investigation for detecting **combinations of different interferences in real time**"; "One of the limitations for researchers is the **lack of publicly available datasets**"; "ML and DL methods still have a **limited use in the industry**"; detection methods that need "a large amount of equipment" are costly, though low-cost components are emerging. — [Radoš et al. 2024](https://www.mdpi.com/1424-8220/24/13/4210)
- A 2025 thesis on DQN multiclass spoofing detection on TEXBAT notes that prior works were mostly binary classification on simulation-based datasets, "with limited attention to real-world data". [thesis, low tier] — [Univ. of Vaasa repository](https://osuva.uwasa.fi/server/api/core/bitstreams/aaa4a445-309b-4a65-8f8a-634a09399edb/content)
- A UAV-navigation security review (Meheretu et al., *J. Aerospace Technology and Management*, 2025, per search snippet) finds that ML and blockchain approaches face scalability challenges and that environmental resilience is underexplored. [J, quartile unverified; full text not opened] — [search result: UTU SLR](https://www.utupub.fi/handle/11111/55991) (note: the UTU entry is a separate systematic literature review on UAV spoofing/jamming; the Meheretu item was only seen in a search summary)

#### B. Alternative navigation (APNT)

**B1. Visual geo-localization / absolute visual localization (AVL) against satellite maps**
- **Couturier & Akhloufi, Drones 2024**: stated challenges: "accurately matching images that may differ in terms of source, time of capture, lighting conditions, and resolution"; "handling dynamic input data with CNNs, which are typically trained offline"; "the absence of large public datasets". **Future directions** (section titles quoted): "Architecture and Loss Function Benchmarking for Large-Scale Matching"; "Fine-Grained Matching" (balance compute vs accuracy); "Hybrid Matching" (few works combine coarse retrieval and fine matching); **"Embedded AVL Implementations. The development and validation of embedded and real-time localization solutions on actual hardware are currently lacking"**; "Hyperspectral AVL" (SWIR for cloud/fog); "Development of Standardized Performance Evaluation Libraries" (no pycocotools-equivalent for AVL); **"Integration of AVL with IMU Technology. IMU data is currently an untapped source..."** — [Couturier & Akhloufi 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)
- **Reported AVL accuracies** (compiled in the same review): Sui et al. 9.80 m (ICRA2022 dataset) and 2.24 m (Wuhan); Mughal et al. ~3.6-3.7 m average but max ~31-33 m; Couturier & Akhloufi Bebop 2 flight ~32.9 m; Bianchi & Barfoot ~1.0-1.5 m RMSE on successful registrations; GLVL 2.39 m (village) vs LocUAV 7.06 m. — [Couturier & Akhloufi 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)
- **NATO STO (Schleiss, Fraunhofer FKIE)**: aerial geo-localization suffers from perspective change, because downward cameras lack a dominant upright orientation, and "purely natural, unstructured scenes, i.e. forests, however, still pose a challenge". [G/C] — [NATO STO MP-SET-275-04](https://www.sto.nato.int/publications/STO%20Meeting%20Proceedings/STO-MP-SET-275/MP-SET-275-04.pdf)
- A survey in *J. National University of Defense Technology* (2026) on low-altitude UAV absolute localization notes remaining limits in "cross-domain generalization, real-time inference on edge platforms, and robustness to complex environments". [J, Chinese; seen via snippet only] — [sciopen](https://www.sciopen.com/article/10.11887/j.issn.1001-2486.25120033)
- SAVL (Remote Sensing 17(14):2408, 2025) addresses UAV-satellite style/season/perspective gaps and reports **8.71 m error at 200 m height over 24 km**. [J, quartile unverified] — [MDPI PDF](https://mdpi-res.com/d_attachment/remotesensing/remotesensing-17-02408/article_deploy/remotesensing-17-02408.pdf)
- Ukraine field note: flat, uniform terrain degrades visual map matching for operators. — [lucorg/BI](https://lucorg.com/?p=19076)

**B2. Visual-inertial odometry (VIO) / SLAM**
- **Jarraya et al., Satellite Navigation 2025, "Challenges"** (quotes/paraphrase): cameras are "significantly impacted by lighting conditions ... low visibility during night-time operations or in foggy environments"; IMUs "suffer from drift"; LiDAR degrades in fog/rain; under "Computational and sensor limitations", "limited processing power and memory onboard UAVs pose challenges in utilizing advanced navigation strategies"; under "Malicious threats", vulnerability to jamming, EMI and **spoofing of alternative navigation sensors**. **Future directions**: "Advanced multi-modal sensor fusion", "Deep learning and AI integration", "Enhancing real-time processing capabilities", and "Addressing implementation barriers" (sensor calibration, data synchronization, environmental adaptation, software integration, power efficiency, scalability). — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)
- That survey's own comparison table says it focuses on outdoor localization and does not cover indoor or path-planning/obstacle-avoidance layers. — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)
- Numbers compiled in Jarraya et al. (the extraction rendered units as "ms"; context indicates metres): PO-MSCKF RMSE 0.28 m (EuRoC MH05), 9.17-14.01 m (KITTI 08/10), 25.47 m (NUDT UAV sequence). Pure VIO drift over km-scale UAV flights is therefore tens of metres. — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)

**B3. Terrain-referenced navigation (TRN/TERCOM/DSMAC)**
- **Jarraya et al. 2025, "Technical limitations"**: "Dependency on terrain features: ... in areas with uniform or featureless landscapes, or where the terrain database is outdated, these methods struggle"; "Initial positioning accuracy: ... TRN systems require accurate initial positioning ... inaccuracies ... can lead to compounded errors". — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)
- Reported numbers: steerable-laser TRN (Carroll & Canciani 2021) improved from ~29-31 m to 10.8/7.9 m (E/N) in flat terrain and to ~1 m in mountainous terrain. LiDAR-based aerial TRN (Hemann et al. 2016) gave 27.2 m final error over ~200 km. — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)

**B4. Learned inertial odometry (IMU-only or IMU+motor)**
- Baseline: Cioffi et al., "Learned Inertial Odometry for Autonomous Drone Racing", *IEEE RA-L* 2023 (TCN + model-based filter, IMU-only on racing drone). Motivation: biases cause "large drift". [J] — [arXiv 2210.15287](https://arxiv.org/pdf/2210.15287v2)
- 2025-2026 preprints: AI-IO (transformer + rotor speed) reports a **36.9% velocity-prediction improvement** [P] — [arXiv 2603.00597](https://arxiv.org/pdf/2603.00597); Massas & Klein neural dead reckoning for quadrotors on **periodic trajectories** [P] — [arXiv 2502.17964](https://www.arxiv.org/pdf/2502.17964); learned IMU bias + invariant filter for real-time VIO, which notes AirIMU "assumes access to ground-truth positions during deployment and does not claim real-time performance" [P] — [arXiv 2505.06748](https://arxiv.org/pdf/2505.06748v2)

**B5. Magnetic anomaly navigation (MagNav)**
- Quantum-magnetometer MagNav field trials (Feb 2025, >6,700 km, up to 19,000 ft): **best final error 22 m (~0.006% of distance)**, ≥11x better than a strategic-grade INS across conditions, with a system small enough for fixed-wing drones. [P, vendor-affiliated, not peer-reviewed] — [arXiv 2504.08167](https://arxiv.org/pdf/2504.08167)
- SandboxAQ/Acubed AQNav (2025): <74 m in a one-hour test over challenging terrain, using the public North American Magnetic Anomaly Map, on a crewed aircraft, not a drone. [N, vendor] — [Quantum Computing Report](https://quantumcomputingreport.com/sandboxaq-and-acubed-announce-results-from-magnetic-navigation-testing-for-aviation/)
- Jarraya et al. cite Cui et al. (2024), LF magnetic-signal positioning with 0.43 m mean error within ~549 m range (this is a beacon-type system, not anomaly-map navigation). — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)

**B6. Signals of opportunity (LEO, cellular)**
- Starlink OFDM-like reference signal structure was "unveiled". A blind receiver tracked six satellites with **6.5 m horizontal error** (static/ground, 2024). The paper won the ION Burka Award 2025. [J/news] — [Kassas et al. PDF](https://people.engineering.osu.edu/media/document/2024-04-15/kassas_unveiling_starlink_leo_satellite_ofdm_like_signal_structure_enabling_precise_positioning.pdf); [OSU ElectroScience news 2026](https://electroscience.osu.edu/news/2026/03/kassas-and-aspin-team-featured-gps-world-cover)
- UAV results are mostly simulated. Differential tightly coupled LEO (14 Starlink + 11 OneWeb) gave 52 cm 3D RMSE vs 12.5 m non-differential (2023, simulation). Real Orbcomm UAV flights gave **75.69 m** 3D RMSE with SGP4 ephemerides, which shows **ephemeris error dominates**. — [Kassas group, orbit-error paper](https://people.engineering.osu.edu/sites/default/files/2023-10/Kassas_Evaluation_of_orbit_errors_and_measurement_corrections_in_differential_navigation_with_LEO_satellites.pdf); [Kassas overview](https://people.engineering.osu.edu/media/document/2022-10-16/kassas_opportunity_comes_knocking_overcoming_gps_vulnerabilities_with)
- Zeng et al. 2026 list "LEO satellite signal navigation enhancement" as a future direction. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)

#### C. Cooperative / relative localization inside swarms without GNSS
- **Tymofieiev & Rogovyi 2025/26 (systematic review)**: "radio-frequency ranging methods offer low computational cost but suffer from **fundamental observability limitations due to the lack of angular information**". Passive visual approaches "achieve high accuracy and global consistency; however, they require substantial computational resources". Active optical markers + distributed factor-graph optimization are a "practically viable compromise". Future direction: "hybrid frameworks capable of dynamically switching between full relative pose estimation and direction-only tracking". — [KhPI Bulletin](https://pm.khpi.edu.ua/article/view/350033)
- A 2022 swarm relative-localization survey flags fully distributed localization as open and proposes linking relative and global localization. [J, Sensors 2022] — [PMC9230124](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9230124/)
- Reference systems: Omni-swarm (decentralized VIO + UWB + visual drone tracking, centimetre-level relative accuracy) — [arXiv 2103.04131](https://arxiv.org/pdf/2103.04131); D²SLAM (decentralized collaborative VI-SLAM; high-precision relative localization "when UAVs are in proximity" plus globally consistent trajectories) — [arXiv 2211.01538](https://arxiv.org/pdf/2211.01538). Both originate in 2021-2022, and I found no clearly newer 2024-2025 flight-validated successor.
- 2025 HIT preprint: swarm localization from communication-signal ranging/channel estimation (spectral clustering + MDS), reducing error in large swarms. Real flights not confirmed. [P] — [arXiv 2509.04412](https://arxiv.org/pdf/2509.04412)
- Zeng et al. 2026, VI-D: swarm-level anti-interference suffers from fusion latency, vulnerable inter-drone links, and loss of redundancy when nodes are compromised. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- Bearing-only passive localization for formations "under electromagnetic silence" (Drones 9(11):767) addresses an EW-specific case: the radio silence that UWB-based schemes cannot satisfy. — cited in [KhPI review reference list](https://pm.khpi.edu.ua/article/view/350033)

#### D. Integrity / trust (knowing when position is wrong) and graceful degradation
- DLR: vision-based navigation can be standalone in GNSS-denied settings, "however, the lack of integrity protections has constrained its utilization in safety-critical applications". [G/research institute] — [DLR ION GNSS+ 2026 exhibit](https://www.dlr.de/en/kn/about-us/departments/navigation/ion-gnss-2026/exhibition/navigation-uav-multi-sensor-and-integrity)
- IM-GIV (arXiv 2410.22672, Oct 2024): integrity monitoring (fault detection + protection level) for tightly coupled GNSS/INS/vision via factor graph optimization. It gives better PLs than LS-RAIM, but "the computation burden is large in some cases". [P] — [arXiv 2410.22672](https://arxiv.org/pdf/2410.22672)
- Li & Waslander (2019): RAIM-style protection levels for optimization-based visual localization give a "significantly more reliable bound than the commonly used 3σ method", which means naive covariance is overconfident. [P/C] — [arXiv 1909.08537](https://arxiv.org/pdf/1909.08537)
- Cranfield (Tabassum, Petrunin, Rana 2022): failure-mode analysis for VIO in urban environments, with federated-filter fault detection. — [Cranfield DSpace](https://dspace.lib.cranfield.ac.uk/items/1dd63788-21d6-4d1d-b747-eed97efe1e6e/full)
- In a 2026 preprint (NGPS), satellite-match covariance is set heuristically from RANSAC inlier ratio, reprojection error and match confidence. This shows the current practice of hand-tuned uncertainty for visual absolute fixes. [P] — [arXiv 2607.18936](https://arxiv.org/abs/2607.18936)
- Jarraya et al. 2025 list "spoofing of alternative navigation sensors" as a malicious threat. Integrity therefore has to cover vision and other APNT sensors, not just GNSS. — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)

### Inferences
- **Generalization gap (detection):** published 95-99.9% detection rates are not evidence of field robustness. Zeng et al. explicitly flag out-of-distribution failure, and Radoš et al. flag lack of public real-world data.
- **Jamming and spoofing are handled separately, and detection is separate from navigation response.** The survey call for "unified end-to-end detection-mitigation" plus "GNSS-centric multisource fusion" means no standard pipeline exists yet that uses a spoofing flag to re-weight VIO/AVL in real time.
- **AVL is the most active and most field-relevant APNT branch**, but it has a well-documented "lab-to-flight" gap: few embedded real-time validations, weak performance on forests and flat or uniform terrain and across seasons, and no standard evaluation library.
- **Integrity for vision-based APNT is immature.** Calibrated, cheap protection levels for visual/AVL fixes are an open problem connecting sub-problems B and D.
- **Swarm relative localization:** UWB lacks bearing, vision is heavy, and EW makes radio emission risky, which pushes toward passive (vision/bearing-only/optical marker) hybrids. Flight-validated, decentralized systems are still mostly 2021-2022 vintage.
- MagNav and LEO SoOP are promising but immature for small UAVs: MagNav needs sensitive magnetometers and platform-noise compensation, and is vendor-led; LEO UAV results are mostly simulated or limited by ephemeris.

### Gaps
- I could not open the full IEEE TAES, NAVIGATION (ION), or GPS Solutions 2024-2026 surveys (publisher domains were unreachable from this environment). Survey extracts above come from COMST, Satellite Navigation, Drones, Sensors and the KhPI review.
- No high-tier (Q1/Q2) 2024-2026 survey dedicated to aerial-swarm relative localization was found. The only recent systematic review found is in a low-tier venue.
- No 2024-2026 survey specifically on integrity monitoring for vision-based UAV navigation was found.
- CRPA weight, power and cost figures for small-UAV-class arrays (e.g., 2-4 element) were not obtained.

---

## Q3. Compute/power constraints: what runs on embedded hardware today (Hz, W, error in m)

### Takeaway
Satellite-image matching fused with VIO now runs in real time on Jetson Orin NX-class boards at 1-2 Hz absolute fixes with ~3 m RMSE at 60-150 m AGL. VIO runs at 10-20 Hz and the IMU at 100-200 Hz. Watt-level power figures and sub-10 W (Raspberry Pi/MCU-class) results are largely missing from the 2024-2026 literature I found.

### Cited Findings
- **NGPS** (Sharma, arXiv 2607.18936, 21 Jul 2026): satellite-image deep matching + VIO + IMU in a UKF with confidence-weighted covariance; **absolute fixes 1-2 Hz, VIO 10-20 Hz, IMU 100-200 Hz**; **2.94 m position RMSE**, worst-case ATE 6.04 m at 150 m AGL and 2 m/s, a 3.5x improvement over monocular VIO; real flights (5 sequences, 60-150 m AGL); **real time on NVIDIA Jetson Orin NX**. Power not reported. Code partly open (github.com/snktshrma/ngps_flight). [P] — [arXiv 2607.18936](https://arxiv.org/abs/2607.18936)
- **PiLoT** (arXiv 2603.20778, 2026): registers live video to a geo-referenced 3D map; median error **1.37 m at 30-40 ms/frame**, 100% success across day-night and cross-season tests (per snippet; hardware not confirmed). [P] — [arXiv 2603.20778](https://arxiv.org/pdf/2603.20778.pdf)
- GLVL (2023): 2.39 m in sparse-texture village scene at **0.48 s per localization** (~2 Hz). — [cited via search summary; also in Couturier & Akhloufi 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)
- Couturier & Akhloufi's own AVL ran with a UAV monocular camera at **1 Hz**, with ~32.9 m error on a Parrot Bebop 2 flight. — [Drones 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)
- Jarraya et al. 2025 compile rates: Isaac ROS Visual SLAM up to **250 Hz** (GPU-accelerated); VINS-Mono 20-25 Hz camera / 200 Hz IMU; they mention NVIDIA Jetson by name **without** benchmark numbers. — [Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)
- Most recent systematic VIO-on-Jetson benchmark found: Jeon et al., "Run Your Visual-Inertial Odometry on NVIDIA Jetson", IEEE RA-L/ICRA 2021. It covers TX2, Xavier NX and AGX Xavier, with VINS-Mono, VINS-Fusion, Kimera, ALVIO, ROVIO and others, and reports accuracy, CPU and memory, but **not Orin-class, Raspberry Pi, or power**. — [arXiv 2103.01655](https://arxiv.org/pdf/2103.01655)
- ML GNSS spoofing detection: an autoencoder at **0.39 s inference** (hardware unspecified in extract). Deep models are flagged as latency/memory bottlenecks needing accelerators. — [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)
- Couturier & Akhloufi: "development and validation of embedded and real-time localization solutions on actual hardware are currently lacking". — [Drones 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)
- IEEE Spectrum's coverage of Ukrainian optical navigation describes neural-network navigation on cheap drones, but exact compute and cost figures could not be retrieved from the article text. — [IEEE Spectrum 2025](https://spectrum.ieee.org/ukraine-killer-drones)

### Inferences
- A realistic embedded operating point for the field today: Jetson Orin NX/Nano class (roughly 10-25 W module class, from general NVIDIA product knowledge, not a source verified here), 1-2 Hz absolute visual fixes, 10-20 Hz VIO, ~3 m RMSE at 60-150 m AGL over texture-rich terrain.
- Missing from the literature: energy-per-fix and W measurements, sub-10 W platforms, and accuracy vs altitude/terrain-type curves on embedded hardware. These are measurable with a hardware prototype.

### Gaps
- No 2024-2026 peer-reviewed benchmark was found reporting **watts** for AVL or VIO on Orin Nano / Raspberry Pi 5 / Hailo / Coral class hardware.
- No embedded-latency figures were found for ML GNSS spoofing detectors running on flight-controller-class MCUs.
- Jetson power envelopes stated above are from general knowledge, not a source fetched in this session.

---

## Q4. Open datasets / benchmarks and what is missing

### Takeaway
Datasets exist for each sub-problem separately (RF interference recordings, AVL image-to-map, multi-UAV UWB/vision). No public dataset was found that combines **real GNSS jamming/spoofing during flight** with **synchronized camera/IMU/raw GNSS** and ground truth, or a **multi-UAV** dataset recorded **under GNSS interference**. AVL datasets are concentrated in China at ≤a few hundred m altitude, and lack forest, featureless, snow or night conditions at scale.

### Cited Findings
**GNSS interference (RF / receiver-level)**
| Dataset | Year | Content | Link | Notes |
|---|---|---|---|---|
| TEXBAT (Texas Spoofing Test Battery) | 2012 | Recorded spoofing scenarios (static/dynamic) | cited in [Radoš et al. 2024 refs](https://www.mdpi.com/1424-8220/24/13/4210) (Humphreys et al., ION GNSS 2012) | De facto benchmark; old, GPS L1 only (general knowledge) |
| OAKBAT (Oak Ridge Spoofing and Interference Test Battery) | n/a | Spoofing + interference recordings | listed in [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf) | Year not verified |
| SatGrid | 2020 | Real-time genuine and spoofing GPS traces across locations/conditions | [Radoš et al. refs](https://www.mdpi.com/1424-8220/24/13/4210) | |
| Fraunhofer IIS "GNSS processed interference features"; MFGJ multi-feature jamming dataset; KAIST real-world dataset | — | Jamming features / real recordings | listed in [Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf) | Details not verified |
| UAV Attack Dataset (Ontario Tech) | ~2022-23 | PX4 flight logs, benign + GPS-spoofed (Gazebo sim + live HackRF/GPS-SDR-SIM) | [IEEE DataPort, DOI 10.21227/00dg-0d12](https://ieee-dataport.org/open-access/uav-attack-dataset) | Authors warn the simulated attacks are less accurate; flight-log level only, no RF |
| UND GPS spoofing dataset for UAS | v3 Oct 2022 | Real GPS from a car (≤60 mph) emulating UAS; simplistic/intermediate/sophisticated spoofing | [Mendeley Data, DOI 10.17632/z7dj3yyzt8.3](https://data.mendeley.com/datasets/z7dj3yyzt8/3) | Not airborne |
| HITL UAV DoS/GPS spoofing MAVLink | — | Hardware-in-the-loop MAVLink logs | [IEEE DataPort](https://ieee-dataport.org/open-access/hitl-uav-dos-gps-spoofing-attacks-mavlink) | Simulated |
| Jammertest 2025 dataset (Fraunhofer) | 2025 | Synchronized Innosense + **CRPA** measurements, two outdoor areas; jamming, spoofing, meaconing, chirp, PRN, CW, sweep, multi-emitter; metadata for classification, DF and receiver impact | [Fraunhofer GitLab topic](https://gitlab.cc-asp.fraunhofer.de/explore/projects/topics/Jammer) | Access/licence not confirmed (page timed out) |

**Absolute visual localization (UAV-to-satellite)**
| Dataset | Year | Size / content | Link | Notes |
|---|---|---|---|---|
| University-1652 | 2020 (ACM MM) | 1,652 university buildings; **synthetic** drone + satellite + ground views | [arXiv 2002.12186](https://arxiv.org/pdf/2002.12186) | Synthetic drone views; retrieval-level, not metric localization |
| SUES-200 | — | Cross-view drone-satellite | referenced in [arXiv 2604.01747](https://arxiv.org/html/2604.01747v1) | Details not verified |
| UAV-VisLoc | 2024 | 6,742 drone images, 11 satellite maps, 11 locations in China; lat/lon/alt/date; ~16.4 GB; fixed-wing + multirotor; cross-season | [arXiv 2405.11936](https://arxiv.org/pdf/2405.11936) | China-only; no IMU stream in description |
| AerialVL | 2024 (IEEE RA-L 9(10)) | 11 sequences, ~70 km trajectories, multiple altitudes/routes/times, Qingdao; satellite reference DB; baselines for VPR, alignment, VO | [UDel repository](https://udspace.udel.edu/items/338c0b7c-993b-476c-a095-6820c6f1c031); DOI 10.1109/LRA.2024.3441491 | One region |
| AnyVisLoc | 2025 | ~18,000 low-altitude multi-view images, multiple scenes/altitudes, 2.5D reference maps (NUDT) | via [search summary, arXiv 2503.10692/2504.07836](https://arxiv.org/pdf/2503.10692) | Not independently verified |
| MAFS | 2025 | Multi-altitude flight segments (with SWA-PF method) | via search summary | Not verified |
| ALTO, VTRN (ICRA2022), ATMD, WildNav, Boson-nighttime, DenseUAV, MSDI | various | Listed in Couturier & Akhloufi | [Drones 2024](https://www.mdpi.com/2504-446X/8/11/622/htm) | Boson-nighttime gives thermal/night |
| SatLoc | — | **Not found** in searches | — | Name could not be verified |

**Swarm / multi-sensor (UWB, VIO)**
| Dataset | Year | Content | Link |
|---|---|---|---|
| MILUV | 2025 (IJRR; arXiv Apr 2025; Figshare Feb 2025) | 3 quadcopters, 36 experiments, 217 min; UWB with raw timestamps + **CIR**, up to 12 transceivers, LOS/NLOS; stereo + bottom mono camera, IMU, magnetometer, laser rangefinder, mocap GT; **indoor**, max 4.418 m/s; devkit with VIO, UWB-EKF, CIR-ML baselines | [arXiv 2504.14376](https://arxiv.org/pdf/2504.14376); [Figshare DOI 10.25452/figshare.plus.28386041.v1](https://figshare.com/articles/dataset/MILUV_A_Multi-UAV_Indoor_Localization_dataset_with_UWB_and_Vision/28386041); [GitHub](https://github.com/decargroup/miluv) |
| NTU VIRAL | 2022 (IJRR 41(3):270-280) | Single UAV; 2× 3D lidar, 2 synced cameras, multiple IMUs, 4 UWB nodes on UAV ranging to 3 anchors; 18 sequences indoor/outdoor on NTU campus; prism GT | [project site](https://ntu-aris.github.io/ntu_viral_dataset/); DOI 10.1177/02783649211052312 |

### Inferences
- **Missing #1:** an airborne dataset with real over-the-air jamming/spoofing **plus** synchronized camera, IMU, raw GNSS observables/correlator outputs and independent ground truth. Detection-to-navigation-response research cannot be benchmarked without it. Jammertest is the only plausible legal venue to create one.
- **Missing #2:** an outdoor multi-UAV dataset (MILUV is indoor, NTU VIRAL is single-UAV) with UWB plus vision under GNSS loss, and preferably under RF interference that also affects inter-UAV links.
- **Missing #3:** AVL datasets beyond China. Datasets also lack enough forest, featureless, flat-steppe, snow and seasonal variation, the conditions Ukraine reporting and NATO STO flag as hard. A standard evaluation library is also missing (Couturier & Akhloufi).
- **Missing #4:** benchmarks that report embedded latency and energy alongside accuracy.

### Gaps
- Could not verify the Jammertest 2025 dataset's licence/access or whether earlier Jammertest (2022-2024) raw data are public.
- "SatLoc" dataset not found. GAMMA not found.
- TEXBAT/OAKBAT release details (size, signals) were not re-verified this session.

---

## Q5. Legal constraints, and which gaps are realistically addressable in a 12-16 month master's thesis with hardware

### Takeaway
Over-the-air jamming or spoofing without authorization is illegal in most jurisdictions. Thesis work can avoid transmitting by using recorded datasets (TEXBAT/OAKBAT, Jammertest recordings), conducted (cabled) simulator testing, HIL/SITL injection, or participating in sanctioned events (Jammertest, run by Norway's Nkom). Gaps that fit 12-16 months with a prototype sit at the integration and evaluation layer, not at new RF hardware or quantum sensing.

### Cited Findings
**Legal**
- Finland (Traficom): a permit is needed in advance to own, import or use radio jamming devices; permits can cover scientific research, product development and testing. The Finnish government has proposed criminalizing unauthorized possession of jammers. [G] — [Traficom](https://traficom.fi/en/radio-licences-and-frequencies/use-radio-frequencies/apply-radio-license-radio-jamming-devices); [Finnish Government](https://valtioneuvosto.fi/en/-/1410829/government-proposes-to-criminalise-unauthorised-possession-of-jammers)
- UK: Ofcom states it is "not able to authorise the operational use of jammers"; GPS jamming exercises are a regulated exception. [G] — [Ofcom](https://ofcom.org.uk/spectrum/frequencies/gps-jamming-exercises)
- Jammertest (Andøya, Norway) is organized by Nkom, the Norwegian Communications Authority, with published transmission plans. 2024 ran 9-13 Sept and included spoofing, drone and motorcade scenarios. In 2025 there was CW, sweep and PRN jamming across L1/L2/L5/L6 at up to **50 W**; a less authoritative blog reports ~360 participants from 120 organizations. [G/N] — [Jammertest 2022 transmission plan (Nkom letterhead)](https://gpspatron.com/wp-content/uploads/2022/10/Jammertest-2022-Transmission-plan.pdf); [Jammertest 2024 briefing](https://gpspatron.com/wp-content/uploads/2024/10/Briefing-Jammertest-2024.pdf); [u-blox Jammertest 2025 blog](https://www.u-blox.com/en/blogs/tech/gnss-jamming-spoofing-detection-jammertest-2025-andoya); [GPS World 2024](https://www.gpsworld.com/jammertest-2024-is-underway/)
- The Ontario Tech UAV Attack Dataset includes live HackRF/GPS-SDR-SIM spoofing flights. Its legal framing is not documented in the snippet. It shows that ready-made spoofing data exist and need not be regenerated. — [IEEE DataPort](https://ieee-dataport.org/open-access/uav-attack-dataset)
- The US FCC actively enforces against jammer marketing and use (2026 enforcement document found but not opened). — [FCC DA 26-654A1](https://docs.fcc.gov/public/attachments/DA-26-654A1.pdf)

**Feasibility signals**
- An open-source baseline for satellite-matching + VIO fusion on Jetson Orin NX exists (NGPS, partially open). — [arXiv 2607.18936](https://arxiv.org/abs/2607.18936)
- MILUV ships a devkit with VIO, UWB-EKF and CIR-classification baselines. — [GitHub decargroup/miluv](https://github.com/decargroup/miluv)
- Survey-listed gaps that are explicitly integration or evaluation work: "Embedded AVL Implementations", "Integration of AVL with IMU", "Standardized Performance Evaluation Libraries" ([Couturier & Akhloufi 2024](https://www.mdpi.com/2504-446X/8/11/622/htm)); "unified end-to-end detection-mitigation", "lightweight networks / knowledge distillation", "GNSS-centric multisource deep fusion" ([Zeng et al. 2026](https://cs.newpaltz.edu/~lik/publications/Yejia-Zeng-IEEE-CST-2026.pdf)); "Enhancing real-time processing capabilities", "Power efficiency" ([Jarraya et al. 2025](https://satellite-navigation.springeropen.com/articles/10.1186/s43020-025-00162-z)); RAIM-style integrity for vision ([DLR](https://www.dlr.de/en/kn/about-us/departments/navigation/ion-gnss-2026/exhibition/navigation-uav-multi-sensor-and-integrity); [IM-GIV](https://arxiv.org/pdf/2410.22672)).

### Inferences (feasibility ranking of gap *areas*, not topics)
- **Realistically addressable in 12-16 months with a small-UAV prototype (Jetson/RPi + camera + IMU + COTS GNSS receiver):**
  1. *Embedded, real-time AVL / map-matching + VIO fusion*, evaluated on public datasets (UAV-VisLoc, AerialVL) plus own flights in GNSS-available airspace, with GNSS used only as ground truth. Measuring Hz, W and error vs altitude/terrain addresses the "embedded validation lacking" gap. No transmission needed.
  2. *Integrity / uncertainty calibration for visual absolute fixes and VIO* (protection levels, fault detection, graceful-degradation logic). This can be done on recorded data and own flights.
  3. *Receiver-level GNSS anomaly detection on COTS outputs* (C/N0, AGC, clock bias, NMEA/UBX) with lightweight models. Train and test on TEXBAT/OAKBAT/Jammertest recordings and cross-dataset to expose the out-of-distribution gap. A wired simulator (where available) or SITL/HIL injection avoids over-the-air transmission.
  4. *Swarm relative localization (UWB + vision) on 2-3 small UAVs* using MILUV-style baselines. Feasible, but outdoor multi-UAV flight logistics add risk.
- **Hard within a master's timeline / budget:** CRPA array hardware design (cost, RF lab), quantum MagNav (sensor cost; vendor-dominated), LEO/Starlink SoOP receivers (RF expertise; UAV results still mostly simulated), and generating new over-the-air jamming/spoofing data (legal: requires Jammertest-type authorization).
- **Defense-relevant evaluation conditions that are cheap to include:** flat/uniform terrain, forest, seasonal mismatch, night/thermal, and spoofing of the GNSS *used as initialization* for AVL (the AVL search window depends on a prior position).

### Gaps
- Turkish legal framework (BTK regulations on jamming devices and test authorization) not researched. Check whether any sanctioned GNSS-interference test range exists in Turkey (e.g., military ranges, TÜBİTAK).
- No information found on whether Jammertest accepts university master's students as participants, or on fees.
- No verified figures for the cost of a COTS GNSS simulator (needed for cabled spoofing tests) were collected.
