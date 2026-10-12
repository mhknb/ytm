# Open Application Problems in Autonomous Systems and UAV Swarms for Defense (2024-2026): A Problem Map

Scope note: these notes map *problems* and *gaps* only. They do not propose thesis topics. Quartile labels: "Q? (unverified)" means I did not check Scimago during this session. Labels like "likely Q1 (unverified)" come from prior knowledge and should be checked on scimagojr.com before anyone relies on them.

---

## Q1. Why does each problem matter now? (field evidence and defense relevance)

### Takeaway
Since 2024 the Ukraine war and the US Replicator program have made two things clear. Mass, attritable, cheap drones are central to modern warfare. The bottleneck is software: autonomy, collaboration, and C2 that work under EW and handle heterogeneous fleets. Hardware is not the limiting factor. Replicator's shortfall (hundreds of systems fielded instead of thousands, and trouble procuring software that can command many heterogeneous drones) and Ukraine's move to swarm software that keeps working when GNSS or links are denied both show that coordination, task allocation, and EW-resilient autonomy remain unsolved at operational scale.

### Cited Findings
**Ukraine (field evidence)**
- WSJ (2 Sep 2025) reported a Ukrainian operation in which "a trio of Ukrainian drones flew under the cover of darkness to a Russian position and decided among themselves exactly when to strike." It described Ukraine using AI so that groups of drones coordinate attacks with each other. — [WSJ, MacDonald 2025](https://www.wsj.com/world/ai-powered-drone-swarms-have-now-entered-the-battlefield-2cab0f05)
- Swarmer (Ukrainian startup) says its software has been used in more than 70,000 front-line operations. It cut the crew needed for a drone mission from nine people to three (navigator, mission planner, drone operator). Drones running it can "exchange the targets" and "choose the appropriate payload". Humans stay in a supervisory role. — [Defense One, Tucker, 15 Sep 2025](https://www.defenseone.com/business/2025/09/ukrainian-startup-has-re-invented-drone-swarming/408099/)
- Swarmer claims swarms of up to 25 drones in GNSS-denied environments and plans 100+ drone combined-arms (UAS/USV/UGV) demonstrations. It also states that "Ukraine is slated to deploy close to 5,000,000 drones into active combat" in 2025. (Company press release, so this is self-reported.) — [BusinessWire/Swarmer, 16 Sep 2025](https://www.businesswire.com/news/home/20250916602085/en/Swarmer-Ukraines-Leading-Drone-Autonomy-and-Swarming-Company-Announces-%2415m-Series-A-Led-By-US-Investors)
- Ground and air robots face the same communications dilemma. Radio links can be jammed and fiber-optic tethers can be cut. Overhead UAVs are often used to relay or guide UGVs. — [Defense One 2025](https://www.defenseone.com/business/2025/09/ukrainian-startup-has-re-invented-drone-swarming/408099/)
- Anduril has reportedly built flying mesh networks that relay data across several UAS under heavy EW. Drones "physically reconfigure their geometry to be robust to jamming", for example by triangulating a jammer and repositioning out of its effect. (Single anonymous source, vendor-related.) — [Defense One, Nov 2024](https://www.defenseone.com/technology/2024/11/newest-replicator-drones-proven-battlefields-ukraine/400997/)

**US Replicator (program evidence)**
- Replicator was unveiled on 28 Aug 2023 with the aim of fielding "thousands" of all-domain attritable autonomous (ADA2) systems by Aug 2025. Replicator 2 (announced 27 Sep 2024) focuses on counter-sUAS. CRS notes that swarming "would likely require further advancements in artificial intelligence and/or networked communications to be deployed." — [CRS IF12611](https://www.congress.gov/crs-product/IF12611)
- CRS: "one former defense official noted that DOD had fielded only hundreds by that time" (Aug 2025). Replicator 2 resources were consolidated into JIATF-401 on 27 Aug 2025, and the first Replicator 2 acquisition was announced on 11 Jan 2026. Tranche 1.2 is expected to focus on "software to enable system collaboration". — [CRS IF12611](https://www.congress.gov/crs-product/IF12611)
- Citing WSJ reporting, Responsible Statecraft writes that "the Pentagon struggled to procure software able to command, and attack with, large numbers of different drones". It also mentions integration problems with existing C2, a collision between autonomous boats caused by a software glitch, and drones that failed to launch, missed targets, or crashed in Alaska exercises. Oversight moved from DIU to DAWG (SOCOM). (Advocacy outlet relaying WSJ; treat as secondary.) — [Responsible Statecraft, Oct 2025](https://responsiblestatecraft.org/replicator/)
- Defense News (Jan 2025): officials are "trying to make sure the drones can resist jamming — a huge problem in Ukraine — and how to make the weapons operate in synchrony." — [Defense News, Robertson 2025](https://www.defensenews.com/pentagon/2025/01/14/the-pentagons-replicator-drone-bonanza-faces-an-uncertain-future/)
- CRS cites observers' estimates that Ukraine has used up to 10,000 low-cost attritable systems per month to offset Russian mass. — [CRS IF12611](https://www.congress.gov/crs-product/IF12611)

**Counter-swarm demand signal**
- Army STTR topic ARM26TX04-NV001, "Asymmetric Collaborative Counter Swarm" (up to $300k). Its algorithms run on each UAS, use active comms when the network is permissive, and must "still operate under a denied or degraded network environment by communicating passively." — [Army SBIR/STTR](https://armysbir.army.mil/topics/asymmetric-collaborative-counter-swarm/)
- CNAS "Countering the Swarm" concludes there is "no silver bullet capability that can defeat all drones" and that counter-drone work cannot be left to isolated air-defense formations. — [CNAS](https://www.cnas.org/publications/reports/countering-the-swarm)
- CNA (Jul 2025) documents PLA research and tests of drone swarms (for example, ground launchers deploying 48 fixed-wing drones, and reported 200-drone swarm systems) and PLA work on counter-swarm methods, including naval countermeasures. — [CNA, PRC Concepts for UAV Swarms in Future Warfare](https://www.cna.org/reports/2025/07/PRC-Concepts-for-UAV-Swarms-in-Future-Warfare.pdf)
- NATO ran counter-drone tests at Putlos Training Area, Germany, from 10 to 21 Nov 2025. — [NATO video page](https://www.nato.int/en/multimedia/multimedia/videos/2025/12/01/us-troops-test-counter-drone-technologies-in-germany-to-boost-natos-air-defences)

**Human factors**
- A Finnish Defence Research Agency bulletin (2026) identifies "situation awareness, cognitive load and trust in automation" as the most prominent human-factors issues in human-swarm interaction. — [FDRA Research Bulletin 2026-5](https://puolustusvoimat.fi/documents/1951253/2815786/FDRA_Research_bulletin_2026-5%20(1).pdf/3cab851b-2cd1-2e95-6d6f-5ba106a097ac?t=1780987887692)

### Inferences
- In both Ukraine and Replicator the binding constraint is collaboration software that works across heterogeneous airframes under EW, plus the human-supervision layer. That points research value toward allocation, coordination, and C2 rather than single-drone flight control.
- Swarmer reduced the crew from 9 to 3, but that is still people per mission, not one operator per swarm. The operator-to-drone ratio is still an open operational metric.
- Counter-swarm has grown into a separate program line (Replicator 2, then JIATF-401). Cooperative interception under denied comms is an explicitly funded need, as the Army STTR shows.

### Gaps
- I did not fetch a NATO STO/RTG technical report on swarms (for example, SAS/IST panels). NATO evidence here is limited to an event page.
- I found no independent, quantitative public data on Ukrainian swarm mission success rates. Swarmer's numbers are self-reported.
- The WSJ article is paywalled. Only the lede was available.

---

## Q2. Where do current solutions fall short? (per problem, from 2024-2026 surveys' open-challenge sections)

### Takeaway
Across surveys the same gaps recur: (1) robustness to dynamic events (new tasks, agent loss), (2) communication-constrained or adversarial networks, (3) scalability beyond about 10 agents, (4) sim-to-real transfer and lack of hardware validation, and (5) no standardized benchmarks. Defense-specific gaps add to these: adversarial (learning) jammers, many-vs-many counter-swarm with formal guarantees, graceful degradation, and LLM hallucination and latency in mission planning.

### Cited Findings

#### P1. Dynamic task allocation and re-planning (uncertainty, attrition, heterogeneity)
- **Alqefari & Menai (2025), "Multi-UAV Task Assignment in Dynamic Environments: Current Trends and Future Directions", *Drones* 9(1):75, DOI 10.3390/drones9010075**. Reviews work from 2013 to 2024. Quartile: likely Q1 (unverified). Its "Open Issues and Research Challenges" section lists:
  - *Robustness in dynamic environments*: "Many current solutions lack the robustness needed to handle such unpredictability effectively". Sudden tasks, UAV failures, and changing priorities call for "fault-tolerant mechanisms and adaptive task reassignment strategies."
  - *Scalability*: "Existing algorithms often struggle to maintain performance as the number of UAVs and tasks increases."
  - *Communication constraints*: "delays, bandwidth limitations, and intermittent connectivity … degrade coordination and task allocation performance". It calls for "communication-efficient algorithms … even in constrained or adversarial environments."
  - *Hybrid approaches*: combining centralized and distributed allocation "remains underexplored."
  - *Real-time adaptability*: "Many existing solutions lack the adaptability needed for dynamic reallocation in real-time."
  - *Energy management*: allocation "often neglect[s] energy efficiency in dynamic contexts."
  - *Multi-objective trade-offs* are "complex and often overlooked."
  - *Benchmarking and standardization*: "The lack of standardized benchmarks and evaluation metrics makes it difficult to compare algorithms."
  - In the abstract: market-based methods "face challenges with communication overhead"; intelligent optimization "require[s] significant computational resources"; clustering methods "struggle with adaptability in dynamic environments." — [MDPI Drones 9(1):75](https://www.mdpi.com/2504-446X/9/1/75)
- **Alqudsi & Makaraci (2025), "UAV swarms: research, challenges, and future directions", *J. Engineering and Applied Science* 72:12, DOI 10.1186/s44147-025-00582-3** (Kocaeli Univ.; Q? unverified, probably lower tier). Calls task allocation, motion coordination, and algorithm design that balances "completeness, computational scalability, planning time, and optimality" *advanced challenges*. It also says "as the number of agents increases, the required communication grows exponentially." — [Springer JEAS](https://link.springer.com/article/10.1186/s44147-025-00582-3)
- Further heterogeneous-allocation surveys appeared in search results but were not read: "A Survey on Task Allocation Methods of Heterogeneous UAV Swarms" (ScienceDirect, 2026, pii S2949715926000879; covers static, dynamic, and cross-domain settings) and "Survey on Collaborative Task Assignment for Heterogeneous UAV…" (*AI & Robotics Research*/SciOpen, DOI 10.26599/AIR.2024.9150033). — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2949715926000879); [SciOpen](https://www.sciopen.com/article/10.26599/AIR.2024.9150033)

#### P2. Coordination under degraded or denied comms and EW (communication-aware autonomy)
- **Agent-based anti-jamming survey (arXiv 2508.11687, 2025; preprint)**. Its open challenges are:
  - (a) "Highly Dynamic and Complex Interference Environment". CSI acquisition is "exceptionally challenging", and swarms face both external jamming and "significant mutual interference arising from spectrum sharing within the swarm itself."
  - (b) "Information Uncertainty and Adversarial Intelligence". "Intelligent jammers can learn UAV communication behaviors and flight patterns", which creates an "intelligence versus intelligent interference" dynamic.
  - (c) "Robust and Efficient Decision Algorithm Design". RL "still face[s] fundamental challenges in sample efficiency, safety guarantees, and theoretical robustness."
  - Future direction: "Collaborative Anti-Jamming and Internal Communication Optimization for UAV Swarms" using MARL, distributed spectrum allocation, and low-overhead interference management. — [arXiv 2508.11687](https://arxiv.org/html/2508.11687v1)
- **Catovic, "Anti-jamming and secure communication for UAV swarms in contested environments: a systematic review"** (ArdaScience journal; low-tier or uncertain venue, so treat with caution). Main finding: "every approach discussed here shows measurable gains in simulation, but the field has not yet produced a standardised, layered security architecture that both scales to swarm size and can hold up against an adversary that is itself AI-capable." Its gap table:
  - Gap 2: limited experimental validation.
  - Adversarial adaptation: "DRL defenders are evaluated against static jammers; co-trained adversarial evaluation is absent."
  - Gap 6: "Published MARL results are almost always demonstrated on swarms of four to twelve agents". Scaling to 50 to 200 nodes is unvalidated, "the single most consequential open problem among the AI-related gaps."
  - Gap 7: no standardized benchmarking.
  - Gap 8: "No Framework for Graceful Degradation". It also notes that a link failure can make coordinated action break down "within seconds." — [ArdaScience PDF](http://journals.ardascience.com/index.php/dss/article/download/346/226/1161)
- **Wang et al. (2024), "A Survey on Security of UAV Swarm Networks: Attacks and Countermeasures", *ACM Computing Surveys*, DOI 10.1145/3703625** (likely Q1, unverified). It critiques MARL anti-jamming schemes that "assume that the network and interference models are known, which may not hold in practical scenarios." It also notes that "limited computational resources of UAVs make the algorithms challenging to converge", and that several works assume full CSI or fixed eavesdroppers, which "is not realistic." — [ACM DL](https://dl.acm.org/doi/10.1145/3703625)
- "Interference management for UAV swarms" (2025, DOI 10.7527/S1000-6893.2025.32022). The DOI prefix indicates *Acta Aeronautica et Astronautica Sinica*, not *Chinese Journal of Aeronautics*. It describes interference that is coupled across the communication, sensing, and control layers, including spatiotemporal inconsistency of heterogeneous sensing data caused by latency, and says these effects "undermine the robustness of UAV swarm task execution." — [SciOpen](https://www.sciopen.com/article/10.7527/S1000-6893.2025.32022)
- Representative 2024 Q-journal work: *Drones* 8(10):558 (2024) covers robust multi-UAV trajectory and power control against jammers whose location and power are uncertain. It notes that existing studies "primarily address the uncertainty in the locations of jammers" and "rarely explore the energy constraints of a UAV swarm." Validation is simulation only. — [MDPI Drones 8(10):558](https://www.mdpi.com/2504-446X/8/10/558)
- Ekechi et al. (2025) note that constrained communication bandwidth is often "not modeled or discussed" in MARL-UAV papers. — [MDPI Drones 9(7):484](https://www.mdpi.com/2504-446x/9/7/484)
- Existence proof for comm-free coordination: Horyna et al. (2023), "Decentralized swarms of UAVs for search and rescue operations without explicit communication", *Autonomous Robots* 47:77-93, DOI 10.1007/s10514-022-10066-5 (cited in Alqudsi & Makaraci 2025). — [Springer JEAS reference list](https://link.springer.com/article/10.1186/s44147-025-00582-3)

#### P3. Counter-swarm / C-UAS with cooperative interceptors; pursuit-evasion
- **Sherman, Shao, Sun, Zheng, Ellis (2024), "Counter UAV Swarms: Challenges, Considerations, and Future Directions in UAV Warfare", *IEEE Wireless Communications*** (likely Q1, unverified). They name "a robust communication infrastructure" as a prime challenge and show how UAV-to-UAV latency hurts MARL interception of a faster target, with preliminary numerical results only. — [NSF PAR](https://par.nsf.gov/biblio/10540521-counter-uav-swarms-challenges-considerations-future-directions-uav-warfare)
- **Xu, Yang (2025), "New Explorations in Autonomous Low-Altitude Area Defense Decision-Making and Control Methods of UAV Swarms", *Guidance, Navigation and Control* (World Scientific), DOI 10.1142/S2737480725030013** (Q? unverified). It finds that "traditional differential games struggle with scalability and MARL approaches face stability and interpretability issues". Open challenges: "mapping biological behaviors to UAV rules, modeling maneuverability with environmental constraints, and inferring intent for mission planning". It calls for "formal control guarantees" in "many-vs-many defense scenarios where existing methods fall short." — [World Scientific](https://www.worldscientific.com/doi/10.1142/S2737480725030013)
- **Valianti, Malialis, Kolios, Ellinas (2024), "Cooperative Multi-Agent Jamming of Multiple Rogue Drones Using RL", *IEEE Trans. Mobile Computing*, DOI 10.1109/TMC.2024.3409050** (likely Q1, unverified). Pursuer UAVs jointly optimize mobility and jamming power while keeping self-interference below a threshold. Evaluation is "extensive simulation". — [ACM DL mirror](https://dl.acm.org/doi/10.1109/tmc.2024.3409050)
- **Anti-UAV perception survey (arXiv 2504.11967, 2025; preprint)**. "Our analysis reveals persistent gaps in real-time performance, stealth detection, and swarm-based scenarios". UAVSwarm "includes up to 23 drones", while "testing on larger fleets (50+) remains uncommon". "Stealth or jamming scenarios … are still sparsely represented in open-source datasets." Extending multi-object trackers to swarms "remains challenging due to association uncertainty." — [arXiv 2504.11967](https://www.arxiv.org/pdf/2504.11967v2)
- **RL for decision-level interception prioritization (arXiv 2508.00641, 2025; preprint)**. Prior work "often assume[s] fully observable, static environments, failing to model the uncertainty and partial observability typical of real-world threat response". Its listed future work includes multi-defender coordination under partial observation and decoys or stealth drones. Code is public. — [arXiv 2508.00641](https://arxiv.org/html/2508.00641)
- Shepherd Grid Strategy (arXiv 2508.09536, preprint) reports more than 95% interception versus 65% for traditional methods, in simulation only. It criticizes existing methods for "static coordination strategies, absence of hierarchical role assignment, and lack of seamless operational phase transitions." — [arXiv 2508.09536](https://arxiv.org/html/2508.09536)
- MDPI *Engineering Proceedings* 133(1):164 (conference-level) covers cooperative counter-drone swarms with MAPPO. — [MDPI Eng. Proc.](https://www.mdpi.com/2673-4591/133/1/164)

#### P4. Collaborative perception and distributed search and tracking
- **U2UData (Feng, Wang, Han, Zhang, Zhu; ACM MM 2024)**. "Cooperative perception is mainly focused on the vehicles and ignores the UAV literature, which remains challenging to validate U2U perception in real-world scenarios due to the lack of public datasets". Prior UAV datasets use one terrain, one weather condition, fixed altitudes and formations, so "there will be a clear domain gap between existing synthetic data and real-world data." — [arXiv 2408.00606](https://arxiv.org/html/2408.00606)
- **U2UData+ (2025, preprint)**. U2UData trajectories are "only 15 seconds" and cover only basic perception and tracking. Embodied long-horizon tasks "require handling long-term dependencies, maintaining persistent states, and adapting to dynamic goal shifts". Benchmarks show intermediate fusion beats late fusion by up to 27.48% AMOTA, yet absolute AMOTA stays low (≤24.6). — [arXiv 2509.00055](https://arxiv.org/html/2509.00055)
- **CoPeD (arXiv 2405.14731)**: multi-robot collaborative perception "remains largely unexplored". It involves fusing "compressed, intermittent, limited, heterogeneous, and asynchronous" information, and "one major hurdle has been the lack of real-world datasets." — [arXiv 2405.14731](https://arxiv.org/pdf/2405.14731)
- **AirV2X (2025)**: existing air-ground datasets are "restricted to minimal agent configurations (typically one vehicle with one or two drones)." — [arXiv 2506.19283](https://arxiv.org/html/2506.19283v2)

#### P5. Human-swarm teaming, workload, explainability, meaningful human control, LLM mission specification
- **"Towards human-centered interaction with UAV swarms: Framework, system design, and user study"** (Elsevier, 2025; pii S3050741325000291; journal title and quartile unverified). "Technical and ethical constraints mean that the role of human operators in command decision-making, intent expression, and anomaly handling remains indispensable". Central challenges include "cognitive-friendly interaction mechanisms, reduction of operator workload, enhancement of information visualization". Under "one-to-many" control, operators "must frequently switch between individual drones or sub-swarms", which brings a risk of "cognitive overload and loss of situational awareness." — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S3050741325000291)
- "Effects of Swarm Size Variability on Operator Workload" (arXiv 2604.21707, 2026, preprint) studies swarm-size transitions, which are directly relevant to attrition. — [arXiv 2604.21707](https://arxiv.org/html/2604.21707v1)
- Gackowska-Kątek & Cofta (2024), "Explainable machine learning model of disorganisation in swarms of drones", *Scientific Reports* 14:22519, DOI 10.1038/s41598-024-73220-2. — cited in [ScienceDirect HSI paper](https://www.sciencedirect.com/science/article/pii/S3050741325000291)
- **"Large Language Models for Multi-Robot Systems: A Survey" (arXiv 2502.03814 v5; preprint)**. Limitations: "mathematical reasoning limitations, hallucination, latency issues, and the need for robust benchmarking". LLM-plus-solver pipelines suffer when "LLM-generated structures are plausible yet semantically wrong, causing solvers to compute optimal solutions to the wrong problem". "LLMs tolerate deliberative latency only at low frequencies". "Scalability to large fleets remains unvalidated. Most experiments involve small teams, typically fewer than ten robots". Fixed communication policies "degrade in dynamic environments." — [arXiv 2502.03814](https://arxiv.org/html/2502.03814v5)
- **MLLM-enabled UAV swarm (arXiv 2506.12710, 2025)**: for UAVs, hallucinations "can result in crashes or collateral damage". It discusses the trade-off between CoT length and latency and notes that outdoor link blind spots undermine centralized LLM inference. — [arXiv 2506.12710](https://arxiv.org/abs/2506.12710)
- **GenSwarm (Ji et al., 2025; arXiv 2503.23875)** generates code policies from natural language and deploys them on real robots. Generation, deployment, and feedback took about 6, 2, and 2 minutes, so adaptation is "not … real-time". "The validation in most of the aforementioned methods is performed in simulation". The authors list sensing and navigation, and optimality of the generated policies, as limitations. — [arXiv 2503.23875](https://arxiv.org/pdf/2503.23875v2.pdf)
- **LAN2CB (arXiv 2507.16068)**: "no standard dataset exists for evaluating multi-step, long-horizon multi-robot mission execution under natural language". Removing template standardization causes an "average drop of ~15% in success rates", and prior frameworks "face limitations with large robot teams (e.g., ≥10)." — [arXiv 2507.16068](https://arxiv.org/html/2507.16068v2)

#### P6. Safety, verification, sim-to-real, scalability of learned swarm policies
- **Ekechi, Elfouly, Alouani, Khattab (2025), "A Survey on UAV Control with Multi-Agent Reinforcement Learning", *Drones* 9(7):484, DOI 10.3390/drones9070484** (likely Q1, unverified). Section 8, "Open Research Problems":
  - Scalability: MARL works for "small to medium-sized UAV swarms", but "scaling … to larger networks remains a challenge".
  - Real-time learning without "extensive retraining".
  - Control in turbulence.
  - Energy-aware MARL.
  - Transfer learning and generalization.
  - Convergence: "policies trained in a simulation may not converge effectively in the real world due to … the 'reality gap'", and multi-agent non-stationarity "breaks the standard assumptions of RL algorithms." — [MDPI Drones 9(7):484](https://www.mdpi.com/2504-446x/9/7/484)
- A MARL-for-autonomous-systems survey (ResearchGate abstract only) lists "weak sim-to-real transfer, limited interpretability" for UAV swarms. — [ResearchGate](https://www.researchgate.net/publication/400904353_A_Comprehensive_Survey_of_Multi-Agent_Reinforcement_Learning_for_Autonomous_Systems_Algorithms_Applications_and_Open_Challenges)
- Zero-shot sim-to-real exists for decentralized MARL quadrotor formation and pursuit-evasion (Batra et al., 2022, as summarized in arXiv 2508.00641). This shows small-scale transfer is feasible. — [arXiv 2508.00641](https://arxiv.org/html/2508.00641)
- Real-world failure evidence: a software glitch caused an autonomous-boat collision in a Replicator-related test, and drones crashed or missed targets in Alaska exercises (secondary reporting). — [Responsible Statecraft](https://responsiblestatecraft.org/replicator/)

### Inferences
- The six problem areas share one gap: **robustness under realistic, adversarial, non-stationary conditions, validated beyond simulation**. Every survey above ends with some form of "simulation-only, small N, no standard benchmark."
- Allocation (P1) and comms (P2) are tightly coupled. Surveys treat them separately, but the open item named in both is allocation that degrades gracefully under intermittent or adversarial links, with explicit handling of agent loss. Catovic's Gap 8 and Alqefari's robustness item point at the same thing from two directions.
- In counter-swarm (P3), the open frontier has moved from one-on-one interception to many-vs-many under partial observability, with decoys and heterogeneous effectors. Interpretability and formal guarantees are explicitly missing (Xu 2025).
- In LLM mission specification (P5), the consensus architecture (LLM as semantic translator plus a formal or combinatorial solver for correctness) leaves a verification gap at the translation step. That gap ties P5 to P6 safety.
- Agent counts are a recurring weak point: MARL anti-jamming at ≤12 UAVs, LLM-MRS at <10 robots, UAVSwarm at 23 drones. The scalability claims in this literature are largely untested.

### Gaps
- I did not reach the full-text open-challenge sections of IEEE COMST, IEEE TAES, *Chinese Journal of Aeronautics*, *Defence Technology*, *Swarm and Evolutionary Computation*, RAS, or EAAI surveys within the tool budget. Those venues are under-represented here, and a follow-up search should target them specifically, for example "Defence Technology 2024 swarm confrontation survey" and "CJA 2025 UAV swarm cooperative decision survey".
- I found no dedicated 2024-2026 survey on **formal verification or runtime assurance of learned swarm policies** (for example, control barrier functions, shielding, or STL monitoring for MARL swarms). This needs a dedicated search.
- I found no peer-reviewed 2024-2026 survey on **meaningful human control** specific to swarms (legal and ethical side, for example the CCW GGE on LAWS). The FDRA bulletin is the only defense-HSI source here.
- Scimago quartiles were not verified for any venue.

---

## Q3. Evaluation resources: simulators, benchmarks, datasets, and how realistic they are

### Takeaway
Open resources exist for each problem, but they fall into two groups. Some are high-throughput but physically abstract (VMAS, MPE/PettingZoo, SMAC). Others are physically realistic but small-N (gym-pybullet-drones, MILUV, Crazyflie-based testbeds). UAV collaborative-perception datasets are almost all synthetic (CoPerception-UAVs, U2UData, AirV2X). None of them model realistic EW or jamming, or adversarial counter-swarm, which is the defense-relevant gap.

### Cited Findings
- **VMAS** (Bettini et al.): vectorized 2D physics in PyTorch with 12 multi-robot scenarios, "30,000 parallel simulations in under 10s", ">100x faster" than MPE. It is 2D and abstracted, and its authors' group researches sim-to-real with GNNs. — [VMAS page](https://matteobettini.github.io/publication/vmas-a-vectorized-multi-agent-simulator-for-collective-robot-learning/)
- **gym-pybullet-drones** (Panerati et al., "Learning to Fly", PyBullet multi-quadcopter RL gym), plus AirSim, Gazebo, MPE, Multi-Agent MuJoCo, and SMAC (StarCraft). These are the environments the MARL-UAV survey reports in use. The survey gives no aggregate share of works validated on hardware. — [Ekechi et al. 2025, Drones 9(7):484](https://www.mdpi.com/2504-446x/9/7/484)
- **CoPerception-UAVs** (Hu et al., NeurIPS 2022 / Where2comm): 131.9k synchronized images from 5 UAVs at 3 altitudes over 3 towns, AirSim+CARLA co-simulation, synthetic. **CoPerception-UAVs+**: about 10 agents, camera plus depth. — [CoPerception-UAV](https://siheng-chen.github.io/dataset/coperception-uav/); [CoPerception-UAV+](https://siheng-chen.github.io/dataset/CoPerception%2B/)
- **U2UData** (ACM MM 2024): 3 UAVs, 9 km², 315K LiDAR frames, 945K RGB and depth frames, 2.41M 3D boxes, 4 terrains, 7 weather conditions, 8 sensors. Collected in U2USim, a "real-world mapping" simulator modeled on Yunnan, so it is still simulation. Tasks are cooperative 3D detection and tracking. Benchmarks cover When2Com, DiscoNet, V2VNet, V2X-ViT, CoBEVT, and Where2comm. — [arXiv 2408.00606](https://arxiv.org/html/2408.00606); [GitHub](https://github.com/fengtt42/u2udata)
- **U2UData+** (2025): 15 UAVs, 120 h, 600 s traces, long-horizon tasks including task re-allocation, with a closed-loop verification platform. Simulated. — [arXiv 2509.00055](https://arxiv.org/html/2509.00055)
- **AirV2X-Perception** (2025): 6.73 h, up to 5 vehicles, 5 RSUs, and 5 drones, CARLA+AirSim. The paper's table classes UAV3D (2024), U2UData, UVCPNet, and Griffin as "Sim". The only real ones are MAVREC and AGC Drive, each with one drone. — [arXiv 2506.19283](https://arxiv.org/html/2506.19283v2)
- **CoPeD** (2024): real-world heterogeneous air-ground collaborative perception with 3 ground robots and 2 aerial robots, indoor and outdoor, ROS1, all on one 5 GHz Wi-Fi subnet with NTP sync, so communication is idealized. — [arXiv 2405.14731](https://arxiv.org/pdf/2405.14731)
- **MILUV** (Shalaby, Dahdah, Ahmed, Cossette, Le Ny; *IJRR* 45(11), 2026, DOI 10.1177/02783649251405898; likely Q1, unverified): 3 quadcopters, 217 min over 36 experiments, UWB with raw timestamps and CIR (up to 12 transceivers, LOS and NLOS), stereo and bottom cameras, IMU, mocap ground truth. Indoor only, max 4.4 m/s. VIO drifts more than 50 cm on some runs, and some experiments "failed". — [ACM DL/IJRR](https://dl.acm.org/doi/10.1177/02783649251405898); [arXiv 2504.14376](https://arxiv.org/html/2504.14376); [GitHub](https://github.com/decargroup/miluv)
- **Anti-UAV datasets**: DroneRF, Halmstad Drone (RGB, IR, audio), MMAUD (radar plus LiDAR), UAVSwarm (up to 23 drones), Anti-UAV challenge sets. Stealth and jamming scenarios are "sparsely represented". — [arXiv 2504.11967](https://www.arxiv.org/pdf/2504.11967v2)
- **Interception-prioritization simulator** (arXiv 2508.00641): open code and assets, partially observable, heterogeneous threats, effector cooldowns and line-of-sight limits. — [arXiv 2508.00641](https://arxiv.org/html/2508.00641)
- **LLM-MRS benchmarks**: the LLM-MRS survey devotes Sec. 6 to benchmarks and simulators and says robust benchmarking is still needed. LAN2CB states no standard NL long-horizon multi-robot mission dataset exists. — [arXiv 2502.03814](https://arxiv.org/html/2502.03814v5); [arXiv 2507.16068](https://arxiv.org/html/2507.16068v2)
- Catovic's review: the anti-jamming literature uses "a wide range of simulation" setups with no standardized benchmark (Gap 7). — [ArdaScience PDF](http://journals.ardascience.com/index.php/dss/article/download/346/226/1161)

### Inferences
- Realism ladder, roughly: MPE/PettingZoo/VMAS/SMAC (abstract, large N, fast) < gym-pybullet-drones (quadrotor dynamics, small N) < AirSim, Gazebo, U2USim (rendering plus sensors) < real small testbeds (Crazyflie, CoPeD, MILUV).
- None of these resources model **realistic RF channels or jamming** together with swarm control. Communication is usually idealized, as in CoPeD's single Wi-Fi subnet. That missing link between the comms layer and the control layer is itself a benchmark gap.
- MILUV and other UWB-based relative localization data matter for GNSS-denied coordination, which is what Swarmer claims in the field.

### Gaps
- I did not fetch primary pages for **Crazyswarm2**, **PettingZoo**, **SMACv2**, or **gym-pybullet-drones** this session. Their features and versions should be checked from their GitHub repos and papers.
- I found no open benchmark combining multi-UAV task allocation, agent attrition, and jamming. If one exists (for example, in the SMAC-like UAV benchmarks the brief mentions), I did not find it.
- I found no quantitative meta-analysis of the share of swarm papers with hardware validation. Surveys assert "simulation-dominant" qualitatively only.

---

## Q4. Which gaps are realistically addressable in a 12-16-month master's thesis with a small hardware demonstrator (3-5 small drones or ground nodes)?

### Takeaway
The gaps a master's project can realistically reach are the ones whose failure modes already show up at N = 3-5 and that do not need large swarms or military RF hardware. These are: robustness of allocation to agent loss and intermittent links; small-N sim-to-real of learned coordination policies; comm-budgeted collaborative perception and tracking; and verified LLM-to-mission translation with a human in the loop. Gaps that are out of reach are: scaling claims (50-200 agents), realistic adversarial EW (which needs licensed RF), and full counter-swarm kinetic interception.

### Cited Findings
- Small-N hardware results are still publishable and called for. MARL anti-jamming studies use only 4-12 agents. LLM-MRS experiments use fewer than 10 robots. MILUV and U2UData each use 3 UAVs. — [ArdaScience PDF](http://journals.ardascience.com/index.php/dss/article/download/346/226/1161); [arXiv 2502.03814](https://arxiv.org/html/2502.03814v5); [arXiv 2504.14376](https://arxiv.org/html/2504.14376); [arXiv 2408.00606](https://arxiv.org/html/2408.00606)
- Surveys explicitly call for "fault-tolerant mechanisms and adaptive task reassignment strategies", "communication-efficient algorithms", hybrid centralized/distributed allocation, and realistic benchmarks. — [Drones 9(1):75](https://www.mdpi.com/2504-446X/9/1/75)
- Field systems already run with 3-drone teams and a human supervising (the Ukrainian "trio" strike and Swarmer's 3-person crew), so N = 3-5 is operationally meaningful. — [WSJ](https://www.wsj.com/world/ai-powered-drone-swarms-have-now-entered-the-battlefield-2cab0f05); [Defense One](https://www.defenseone.com/business/2025/09/ukrainian-startup-has-re-invented-drone-swarming/408099/)
- The Army STTR requires algorithms that work in both permissive and "denied or degraded" networks by "communicating passively". That requirement can be emulated in the lab with packet dropping and bandwidth caps. — [Army SBIR](https://armysbir.army.mil/topics/asymmetric-collaborative-counter-swarm/)
- GenSwarm and LAN2CB show the LLM-to-code-to-real-robot pipeline running on small real fleets, and both name an open benchmark gap. — [arXiv 2503.23875](https://arxiv.org/pdf/2503.23875v2.pdf); [arXiv 2507.16068](https://arxiv.org/html/2507.16068v2)
- Open simulators with sim-to-real lineage are available, such as VMAS and gym-pybullet-drones. — [VMAS](https://matteobettini.github.io/publication/vmas-a-vectorized-multi-agent-simulator-for-collective-robot-learning/); [Drones 9(7):484](https://www.mdpi.com/2504-446x/9/7/484)

### Inferences (feasibility assessment; not topic proposals)
- **High feasibility (fits 3-5 nodes):**
  - Allocation and re-planning under emulated link loss and agent removal (P1+P2). The failure modes are reproducible at small N, and communication degradation can be emulated in software (drop rate, latency, bandwidth).
  - Small-N sim-to-real of a learned coordination policy (P6), with quantified reality-gap metrics.
  - Bandwidth-limited collaborative tracking with 3 nodes (P4), using existing fusion baselines such as Where2comm or When2Com, possibly with ground nodes or cameras as stand-ins.
  - LLM mission specification with a formal checking layer and operator-workload measurement (P5+P6), using simple user studies.
- **Medium feasibility:**
  - Cooperative pursuit and interception of one evader by 2-4 pursuers indoors (P3), which is safe with nano-drones and nets or virtual capture.
  - HSI workload studies, which need ethics approval and participants.
- **Low feasibility for a master's project:**
  - Credible scalability claims (50+ agents). Simulation only, and hard to make novel.
  - Real RF jamming experiments, which need legal and spectrum authorization. Emulation is the realistic substitute.
  - Many-vs-many counter-swarm on hardware.
  - Outdoor GNSS-denied swarms, because of regulation, safety, and cost.
- **Risk:** at N = 3-5, reviewers may say "this doesn't scale". The usual mitigation is a combined design: large-N simulation (VMAS or gym-pybullet-drones) plus small-N hardware to validate the reality gap.

### Gaps
- I did not verify the cost or availability of specific platforms (Crazyflie 2.1 plus Crazyswarm2, Tello EDU, PX4-based small quads) or indoor localization requirements (mocap, UWB, Lighthouse) in this session.
- I found no source that quantifies typical master's-thesis scope in swarm robotics. The feasibility judgments above are my own reasoning, not cited.
