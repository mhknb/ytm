# Emerging Methodological Approaches (2024-2026) for Multi-Agent Autonomy and UAV Swarms: Maturity and Open Methodological Gaps

Scope note: notes cover method families only (no thesis topics). Quartiles: I did NOT verify any Scimago/WoS quartile directly during this session. Where a quartile is given it is marked "(SJR Q?, unverified)" and should be checked on scimagojr.com before citing. Venue status of arXiv items is marked "preprint" unless a venue was confirmed in the source. Maturity labels used: L1 = simulation only; L2 = HIL / lab hardware (mocap, Crazyflie); L3 = outdoor multi-UAV flight; L4 = fielded/operational (none of the learning methods below reached L4 in the sources found).

Defense-problem codes used in "applied / not applied" lines: TA-A = task allocation under attrition; CDC = communication-denied coordination; CS = counter-swarm / swarm confrontation; CP = collaborative perception; GCL = GNSS-denied cooperative localization; HST = human-swarm teaming.

---

## Q1. Multi-agent reinforcement learning (CTDE, MAPPO, mean-field, attention/Deep Sets for variable team size, hierarchical MARL)

### Takeaway
MARL under CTDE (MAPPO/QMIX-family, attention critics) is the dominant learning paradigm for swarm decision-making in 2024-2026 literature, and scale-invariant architectures (attention, GNN, mean-field) are the main route to variable team size; however surveys agree it remains fragmented, mostly simulation-validated, with scalability, sim-to-real, sparse rewards and benchmark inconsistency as standing gaps. Zero-shot transfer across swarm sizes works "functionally" but degrades measurably beyond ~2x the training size.

### Cited Findings
**Plain-words definition.** CTDE = agents are trained with access to global information (a centralized critic) but execute with only local observations; MAPPO = PPO extended to this setting; mean-field MARL = each agent reasons about the *average* action of its neighbours instead of every neighbour, so input size does not grow with swarm size; attention / Deep Sets / GNN encoders = permutation-invariant network layers that accept a variable number of neighbours.

Surveys / open challenges
- Ekechi, Elfouly, Alouani, Khattab, "A Survey on UAV Control with Multi-Agent Reinforcement Learning," *Drones* 9(7):484, 2025, DOI 10.3390/drones9070484 (SJR Q1/Q2?, unverified). States the field "remains fragmented, with a wide variety of algorithms, architectures, and evaluation metrics spread across domains"; policy-based MARL faces "scalability to large agent populations, efficient communication protocols, and robustness to partial observability"; future work toward "scalable architectures, incorporating meta-learning for adaptability, and designing algorithms that can operate effectively with limited communication." It critiques reviewed works for "the lack of a realistic scenario, and limited evaluation against benchmarks such as QMIX, MADDPG, and MAPPO." — [MDPI](https://www.mdpi.com/2504-446X/9/7/484); [ADS record](https://ui.adsabs.harvard.edu/abs/2025Drone...9..484E/abstract)
- Same survey's comparison table: Transformer-based MARL reported highest coverage (97%) with high scalability; centralized MADDPG 95% target coverage but "limited fault tolerance"; one threat-aware framework required ">150,000 steps." — [MDPI](https://www.mdpi.com/2504-446X/9/7/484)
- Wang, "Reinforcement Learning-Based Methods for Cooperative Control of UAVs: Challenges and Perspectives," *Guidance, Navigation and Control* (World Scientific), 2025, DOI 10.1142/S2737480725030037 (quartile unverified): names "model update synchronization to maintain spatiotemporal consistency between simulations and their physical counterparts" as "the foremost challenge in collaborative UAV training environments." — [World Scientific](https://www.worldscientific.com/doi/10.1142/S2737480725030037)
- Older but frequently cited baseline: Frattolillo et al., "Scalable and Cooperative Deep Reinforcement Learning Approaches for Multi-UAV Systems: A Systematic Review," *Drones* 7(4):236, 2023 — flags exponential growth of state/action spaces with agent count and sim-to-real transfer as key limits. — [MDPI](https://www.mdpi.com/2504-446X/7/4/236)

Variable team size / scale invariance
- Aguzzi, Domini, Venturini, Viroli, "Scaling Swarm Coordination with GNNs—How Far Can We Go?", 2025 (venue not confirmed in source): GNN-based Deep Graph Q-Learning trained on 10 agents transfers to 15-29 agents "preserving coordinated behavior and safety (near-zero obstacle collisions)" but "efficiency declines monotonically" and "worsens beyond roughly twice the training size (≈20 agents)"; authors state zero-shot population scaling "remains largely unexplored" and mean-field methods "rely on strong homogeneity assumptions." — [Exa library record](https://exa.ai/library/publication/k9b2jb00ztv)
- Lin & Lee, "HGAP: Boosting Permutation Invariant and Permutation Equivariant in MARL via Graph Attention Network," ICML 2024, PMLR 235:30189-30210 — graph attention policy enforcing PI/PE; benchmarks only (no UAV hardware). — [PMLR](https://proceedings.mlr.press/v235/lin24m.html)
- Chen, Song, Mo, Lv, Yu, "Scalable Cooperative Decision-Making in Multi-UAV Confrontations: An Attention-Based Multiagent Actor-Critic Approach (AMAAC)," *IEEE Trans. Aerospace and Electronic Systems*, 2025 (SJR Q1?, unverified): multi-head attention + self-play in CTDE; observation encoder and attention critic "adapt to varying number of UAVs"; strategies generalize "even beyond the training scenario's scale"; beats MAPPO, MAHPG, SECA on win and kill-death ratios (simulation). — [Exa library record](https://exa.ai/library/publication/7vd5ck2yjjb)
- Yan et al., "MARL With Spatial-Temporal Attention for Flocking With Collision Avoidance of a Scalable Fixed-Wing UAV Fleet (STAAC)," *IEEE Trans. Intelligent Transportation Systems*, 2024/2025, DOI 10.1109/TITS.2024.3505929 (SJR Q1?, unverified): population-invariant attention network adapts to changes in fleet size and number of non-cooperative intruders; validated in simulation and hardware-in-the-loop. — [ACM DL mirror](https://dl.acm.org/doi/10.1109/TITS.2024.3505929)
- Mean-field: "Large-scale UAV swarm path planning based on mean-field reinforcement learning" (PO-WMFDDPG), *Chinese Journal of Aeronautics* 38(9), 2025, DOI 10.1016/j.cja.2025.103484 (SJR Q1?, unverified): partially-observable weighted mean-field DDPG; simulation-only, higher success/convergence than DDPG and MFDDPG. — [SciOpen](https://www.sciopen.com/article/10.1016/j.cja.2025.103484)
- Mean-field actor-critic for large UAV networks (UCL, *IEEE TCCN* accepted version, 2025): critic input reduced from M+KP to M+2P, "independent of the agent population size"; 80% fewer episodes, 70% less training time vs. MFDQN. — [UCL Discovery PDF](https://discovery.ucl.ac.uk/id/eprint/10219522/1/6.TCCN-TP-25-0629-final%20version.pdf)
- GPMF (graph attention + partially observable mean field), *Drones* 7(7):476, 2023 — explicitly models "the death scene of the agent" (agent loss) in large-scale cooperative roundup; MAgent simulation only. — [MDPI](https://www.mdpi.com/2504-446X/7/7/476)
- Fu, "Group Symmetric Networks for Scalable Multi-Agent Drone Navigation," 2025: symmetry-aware attention; +44.0% sample efficiency, +25.6% completion vs MAPPO, but only "at 6-agent scales." — [Exa library record](https://exa.ai/library/publication/pzk1d8zmh3m)

Hierarchical MARL
- "HMARL-CBF – Hierarchical MARL with Control Barrier Functions for Safety-Critical Autonomous Systems," NeurIPS 2025: high level learns joint policy over skills, low level learns safe skill execution with CBFs; evaluated on road-network navigation, not UAVs. — [NeurIPS PDF](https://papers.nips.cc/paper_files/paper/2025/file/76486c7eb6056f12e7ce3addced61650-Paper-Conference.pdf)
- Hierarchical rule/HMM-intent + QMIX defense model for drone swarm confrontation (*Journal of Shanghai Jiao Tong University*, 2025): hierarchical > single-layer on every index; Python+Unity simulation. — [SJTU journal](https://www.qk.sjtu.edu.cn/ktfy/EN/abstract/abstract50436.shtml)
- "Learning-Based Multi-Robot Active SLAM: A Conceptual Framework and Survey," *Applied Sciences* 16(3):1412, 2026: concludes "Hierarchical Reinforcement Learning (HRL) and graph-based spatial abstraction currently offer superior scalability and robustness compared to monolithic end-to-end approaches." — [MDPI](https://www.mdpi.com/2076-3417/16/3/1412)

Onboard feasibility
- LEARN (Learning End-to-End Aerial Resource-Constrained Multi-Robot Navigation), arXiv 2511.17765, 2025 (preprint; venue not confirmed): compact attention-based RL policy + low-res ToF sensors, designed for "single-core processors operating below 1 GHz," "onboard memory of less than 1 MB," and "wireless communication bandwidth below 10 MHz"; fully onboard flight on six Crazyflies at up to 2.0 m/s through 0.2 m gaps; +10% vs two SOTA planners in sim. — [ar5iv](https://ar5iv.labs.arxiv.org/html/2511.17765)

### Inferences
- Maturity: CTDE/MAPPO + attention is L1-L2 for most swarm decision tasks; low-level navigation policies have reached L2-L3 (LEARN on Crazyflie, CATA/TACC on 10 fixed-wing UAVs — see Q3). Mean-field methods remain L1 in the UAV literature found.
- Onboard: small MLP/attention policies run on microcontroller-class hardware (LEARN <1 MB); GNN/attention critics are only needed at training time under CTDE, so execution cost is usually small. The open issue is not inference cost but observation/communication assumptions at execution.
- Defense coverage: CS (confrontation) is heavily studied in simulation (AMAAC, MARL-LAC, GPMF); TA-A only partially (GPMF models agent death; few works test policy robustness when agents are removed mid-mission); CDC addressed indirectly via "without communication" CTDE policies; GCL, HST almost absent from MARL swarm papers found.
- A methodological gap visible across sources: scale generalization is evaluated with growth of team size (more agents) but rarely with *shrinkage under attrition during an episode* plus heterogeneity simultaneously.

### Gaps
- No 2024-2026 MARL-UAV survey reporting a quantitative share of real-flight vs. simulation papers was found (Ekechi et al. classify environment type but I did not retrieve the counts).
- Could not verify whether LEARN was accepted at a peer-reviewed venue.
- Did not find a 2024-2026 hierarchical-MARL paper validated on real multi-UAV hardware for defense tasks.

---

## Q2. Graph neural networks and learned communication (when/what/whom to communicate, bandwidth-aware, robust to loss/adversarial messages)

### Takeaway
Learned communication (Comm-MARL) is well theorised — when/whom/what to send, gating, graph-generated topologies — and robustness to adversarial/lost messages has a dedicated 2024-2025 literature (certified ensembles, adversarial training, decentralization), but these are almost entirely evaluated on generic MARL benchmarks; UAV-specific, hardware-validated learned-communication work is rare (CATA/TACC is the notable exception).

### Cited Findings
**Plain-words definition.** Instead of broadcasting everything, each agent learns (i) a gate deciding *when* to transmit, (ii) a selector deciding *to whom*, and (iii) an encoder deciding *what* compressed message to send; GNN message passing is the natural architecture because swarm communication is a graph.

- Zhu, Dastani, Wang, "A survey of multi-agent deep reinforcement learning with communication," *Autonomous Agents and Multi-Agent Systems* 38, 2024, DOI 10.1007/s10458-023-09633-6 (SJR Q?, unverified): proposes 9 dimensions for classifying Comm-MADRL and focuses on "learning when, how, and what to communicate." — [Springer](https://link.springer.com/article/10.1007/s10458-023-09633-6)
- Standen, Kim, Szabo, "Adversarial Machine Learning Attacks and Defences in Multi-Agent Reinforcement Learning," *ACM Computing Surveys*, 2025, DOI 10.1145/3708320 (SJR Q1?, unverified): execution-time attacks against MARL "are complex due to effects that propagate across time and between agents"; proposes attack-vector framework and identifies knowledge gaps. — [ACM](https://dlnext.acm.org/doi/10.1145/3708320)
- Certifiably robust policy against adversarial communication (arXiv 2206.10158; Sun et al.): attacker may arbitrarily alter messages from any C < (N-1)/2 agents; defense = message-ensemble policy over randomly ablated message sets, certifiably robust "regardless of the attacking algorithm." — [ar5iv](https://ar5iv.labs.arxiv.org/html/2206.10158)
- MA3C (Yuan, Chen, Zhang, Yu), *Frontiers of Computer Science*: auxiliary adversary population generated by evolutionary learning, "every information channel may suffer from distinct message attacks." — [FCS](https://journal.hep.com.cn/fcs/EN/10.1007/s11704-023-2733-5)
- DMAC, arXiv 2504.21278, 2025 (preprint): learned communication tends to concentrate on few channels; "damage of critical communication channels can trigger the crash of the entire system"; adversary masks critical channels during training to force a decentralized structure. — [arXiv](https://arxiv.org/html/2504.21278v1)
- ExpoComm, arXiv 2502.19717, 2025: most comm strategies "are designed for small-scale MASs" and "communication overhead during execution scales quadratically with the number of agents"; proposes exponential-topology communication for many-agent systems. — [arXiv](https://arxiv.org/abs/2502.19717)
- Sparse communication in MADRL, *Neurocomputing*, 2025: existing algorithms "rarely consider the cost during training and execution"; UAVs cited as a case where communication overhead is fundamental. — [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0925231225000165)
- Information-bottleneck communication-efficient MARL for UAV swarms (IB-CEMARL), *Entropy* 28(8):919 (MDPI). — [MDPI](https://www.mdpi.com/1099-4300/28/8/919)
- GNN-for-coordination lineage: Zhou, Sharma, Li, Prorok, Ribeiro et al. "Graph neural networks for decentralized multi-robot submodular action selection"; DGNN-GA (decentralized GNN goal assignment). — [Zhou Lab publications](https://zhourobotics.github.io/publications/); [NSF PAR PDF](https://par.nsf.gov/servlets/purl/10557788)
- UAV-specific: Zhao et al., "Graph-based multi-agent reinforcement learning for large-scale UAVs swarm system control," *Aerospace Science and Technology* 150:109166, 2024, DOI 10.1016/j.ast.2024.109166; and "Graph-based MARL for collaborative search and tracking of multiple UAVs," *Chinese Journal of Aeronautics* 38(3):103214, 2024/2025 (cited inside AMAAC reference list; not read directly). — [AMAAC record listing refs](https://exa.ai/library/publication/7vd5ck2yjjb)

### Inferences
- Maturity: L1 for robust/adversarial comm-MARL (benchmarks such as SMAC/particle environments); L2-L3 only for gating-type communication in task allocation (CATA/TACC, Q3).
- Onboard: message encoders/gates are small; feasible on SoC-class hardware (CATA deployed on Rockchip RK3588). Certified-ensemble defenses multiply inference cost by the ensemble size, an unexamined issue for embedded hardware.
- Defense coverage: CDC partially (gating/sparse comms, loss), adversarial message injection studied generically but NOT on UAV swarms with realistic jamming/spoofing models in the sources found; CP via learned feature sharing is a separate stream (Q5).
- Methodological gap triangulated across sources: robustness work assumes a fixed number of agents and message-level attacks; link-level effects (jamming-induced topology change, latency, asynchrony) are not jointly modelled with adversarial content.

### Gaps
- No 2024-2026 survey specifically on learned communication for UAV swarms (as opposed to generic Comm-MARL) was found.
- Could not confirm the publication venue/year of the certified-robust communication paper (arXiv 2206.10158) or ExpoComm from the retrieved pages.

---

## Q3. Market/auction (CBBA) and optimization methods combined with learning; learning-augmented combinatorial optimization for task allocation

### Takeaway
2024-2026 work hybridises CBBA-style consensus auctions with learning in three ways — learned scoring/bidding (GCN, RL bidders), learned communication gating on top of auctions (CATA/TACC), and end-to-end graph-RL allocators (attention/CAM) — while classic CBBA theory itself is still being repaired (optimality-guarantee flaws, event-driven messaging). CATA/TACC is the most mature: real 10-UAV flight with onboard deployment.

### Cited Findings
**Plain-words definition.** CBBA = each UAV greedily builds a bundle of tasks and bids for them; neighbours exchange winning-bid lists until they agree (consensus) — decentralized, convergent, ≥50% optimal under diminishing-marginal-gain scores. "Learning-augmented" = a neural network replaces the hand-crafted bid, decides when to exchange messages, or directly outputs allocations.

- **CATA** — Xiong, Xi, Cao, Li, Li, Li (National University of Defense Technology), "Communication-Aware Task Allocation for the UAV Swarm via Multiobjective Asynchronous Policy Learning," *IEEE Trans. Aerospace and Electronic Systems* 62:949-966, 2026 (online 28 Oct 2025) (SJR Q1?, unverified): learns a gating policy that times transmissions in a POMDP under CTDE; asynchronous trajectory alignment + Multi-Objective coupled PPO (MOPPO). Vs. ACBBA: −48.48% task conflicts, −79.89% communication overhead, −77.90% convergence time; deployed on RK3588 SoC; ten-UAV search-and-rescue flight. Motivation: existing studies "often assume ideal networks and lack physical validation." — [Exa library record](https://exa.ai/library/publication/h8s6crq0fw9); [dblp](https://dblp.uni-trier.de/rec/journals/taes/XiongXCLLL26.html)
- Conference precursor: Xiong et al., "Bridging the Reality Gap: Communication-Aware Task Allocation with Multi-Objective Asynchronous Policy Learning," IROS 2025 (MOCPPO, primal-dual + PPO, HIL). — [aiconfpaper](https://aiconfpaper.com/paper/iros-2025-XiongZXCWL25)
- **TACC** — same group, "Task allocation with communication coordination in UAV swarms via asynchronous multi-objective policy optimization," *Aerospace Science and Technology* 174:111760, 2026 (SJR Q1?, unverified): constrained MARL (MOCPO, Lagrangian loss) on the gating policy; observation includes channel access, Bron-Kerbosch clique features, Value of Message; states that trade-off between allocation efficiency and transmission overhead via C-MARL "remains an unexplored territory"; HIL + 10 hybrid-wing UAVs (Fei Long-1700) with RK3588-based collaborative controller; fewer conflicts than ACBBA. — [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S1270963826001410); [ADS](https://ui.adsabs.harvard.edu/abs/2026AeST..17411760X/abstract)
- Learned bidding: "Auction-Consensus Algorithm with Learned Bidding Scheme for Multi-Robot Systems," arXiv 2605.21932, 2026 (preprint): CBBA bid replaced by PPO-trained neural bidder (Neural Additive Model, LSTM, Set Transformer), rewards shaped by MILP optimum; NAM ~90% median optimality at 5 agents → ~87% at 20 agents, but with timeout (non-convergence) cases; notes learning-based MRTA "remain[s] sensitive to the training distribution... generalization across environments remains an open challenge." — [arXiv](https://arxiv.org/html/2605.21932)
- Chekakta, Aouf, Govindaraj, Polisano, De Cubber, "Towards Learning-Based Distributed Task Allocation Approach for Multi-Robot System," ICARA 2024, DOI 10.1109/icara60736.2024.10553196: GCN predicts CBBA score function; notes distributed algorithms "assume ideal communication conditions." Follow-up AI-CBBA used in Explosive Ordnance Disposal / landmine detection with UAV + SUGV outdoor tests (AIDED project). — [City Research Online](https://openaccess.city.ac.uk/id/eprint/33240/); [AI-CBBA record](https://exa.ai/library/publication/kw92sp64bj9)
- Theory repair: Kha, Beynier, Labreuche, Marchand, "Enhancing CBBA Convergence and Optimality Guarantees in Multiagent Task Allocation," 2025: CBBA's Time-Discounted Reward is "not always DMG," the 50% guarantee "may not hold even with DMG functions," and idle iterations after convergence; proposes GCBBA. — [Exa library record](https://exa.ai/library/publication/k086bg8t1wy)
- Event-Driven CBBA, arXiv 2509.06481, 2025: event-triggered messaging keeps CBBA bounds while cutting transmissions up to 52%. — [arXiv](https://arxiv.org/abs/2509.06481)
- Attrition-like capability loss: CBPA (Consensus-Based Payload Algorithm), arXiv 2412.10087, 2024: extends CBBA to robots whose capability drops as payload is consumed ("in military confrontation, the strike payload... will be consumed"); future work "enhance fault tolerance." — [arXiv](https://arxiv.org/html/2412.10087)
- Human-in-the-loop auctions: Guillet et al., "Extending Consensus-based Task Allocation Algorithms with Bid Intercession to Foster Mixed-Initiative (I-CBBA)," AAMAS 2025: operators bid on behalf of agents with priority levels, from fully decentralized to fully human-controlled, preserving CBBA convergence; ROS simulation. — [IFAAMAS PDF](https://www.ifaamas.org/Proceedings/aamas2025/pdfs/p932.pdf)
- End-to-end graph RL allocators: Paul & Chowdhury, "Learning to Allocate Time-Bound and Dynamic Tasks to Multiple Robots Using Covariant Attention Neural Networks," *ASME J. Computing and Information Science in Engineering* 24(9):091005, 2024 (scales beyond training size, dynamic tasks); Dai, Bidwai, Sartoretti, ICRA 2024 (coalition formation via RL); heterogeneous MRTA via RL with constrained flashforward, RA-L 2025 (MARMot lab). — [ASME](https://asmedigitalcollection.asme.org/computingengineering/article/24/9/091005/1201342/Learning-to-Allocate-Time-Bound-and-Dynamic-Tasks); [ICRA PDF](https://marmotlab.org/publications/56-ICRA2024-MRTA.pdf); [RA-L PDF](https://marmotlab.org/publications/73-RAL2025-HetMRTA.pdf)
- Expert-guided progressive graph RL for online task allocation of large-scale UAV swarms under constrained communication (SSRN preprint, 2025). — [SSRN PDF](https://papers.ssrn.com/sol3/Delivery.cfm/30aa117c-6fb6-4c94-bf79-d113d5e420c8-MECA.pdf?abstractid=7465061&mirid=1)
- Computational-intelligence survey: "Computational Intelligence Algorithms for UAV Swarm Networking and Collaboration," *IEEE Communications Surveys & Tutorials*, 2024, DOI 10.1109/COMST.2024.3395358 (SJR Q1?, unverified) — classifies task assignment, path planning, search and cooperative jamming algorithms into heuristic-search, policy-design, policy-learning and hybrid categories. — [ACM DL mirror](https://dl.acm.org/doi/10.1109/COMST.2024.3395358)

### Inferences
- Maturity: CBBA itself L3-L4 (widely flown); learned-gating hybrids L3 (CATA/TACC 10 UAVs); learned-bidding and GCN-scoring L1-L2; end-to-end graph-RL allocators L1.
- Onboard: hybrids keep the auction loop (cheap) and add a small network — demonstrated on RK3588 SoC; consistent with embedded deployment.
- Defense coverage: CDC addressed (gating, event-driven); TA-A only indirectly (CBPA capability depletion; no paper found that trains learned bidders/gates with explicit random agent loss and re-auction); HST via I-CBBA (simulation only); CS addressed by auction-based offense/defense allocation in confrontation literature (cited inside MSRM-MAPOCA related work).
- A clear methodological tension: learned bidders can break CBBA's DMG assumption and hence its convergence/optimality guarantee (timeouts observed in the learned-bidding paper; guarantee fragility shown by Kha et al.).

### Gaps
- No source found that formally preserves CBBA convergence guarantees while using a learned (non-DMG) bid function.
- Could not retrieve open-challenge sections of a dedicated 2024-2026 multi-UAV task-allocation survey.

---

## Q4. Sim-to-real transfer, safe RL / control barrier functions, formal verification / runtime assurance

### Takeaway
Crazyflie-scale hardware validation is now routine for safe multi-agent control (GCBF+, layered safe MARL, attention-CBF), and new GPU/JAX simulators enable millions of parallel environments, but outdoor multi-UAV sim-to-real of *decision-level* policies is still limited to a few works, CBF guarantees fragment when many pairwise constraints conflict, and formal verification/runtime assurance for learned swarm policies is thin in 2024-2026 sources.

### Cited Findings
**Plain-words definition.** A control barrier function (CBF) is a mathematical "safety fence": a fast optimization filter minimally modifies the learned controller's command so the state never leaves a safe set (e.g., inter-drone distance > d_min). Sim-to-real = training in simulation then deploying on real drones, typically via domain randomization or digital twins.

- GCBF+ (Zhang, So, Garg, Fan), arXiv 2401.14554 (reported later in IEEE T-RO; venue not confirmed in retrieved page): "graph control barrier function" certificates learned with GNNs; safety proven for arbitrary-sized MAS with a single GCBF; accepts LiDAR point clouds; hardware swarm of drones; up to 20% better than best hand-crafted CBF in Crazyflie-dynamics experiments. — [arXiv](https://arxiv.org/html/2401.14554v4)
- Layered Safe MARL, arXiv 2505.02293, 2025: CBFs/reachability "generally offer rigorous guarantees only when a single safety constraint is considered"; "conflicts between the constraints faced by different agents pose a challenge"; combines MARL with control barrier-value function (HJ reachability) filter; Crazyflie hardware + high-density simulation. — [arXiv PDF](https://arxiv.org/pdf/2505.02293)
- Deep Equivariant Multi-Agent CBFs, arXiv 2506.07755, 2025: learned CBFs "lack in scalability, generalization and sampling efficiency"; equivariant graph CBFs enable "zero-shot generalization to larger and denser swarms" (simulation only). — [arXiv PDF](https://arxiv.org/pdf/2506.07755)
- AttentionSwarm, arXiv 2503.07376, 2025: MAPPO + attention-parameterized CBF; Crazyflie 2.1 with Vicon; 95-100% collision-free in dynamic drone racing — but "centralized multi-agent systems." — [arXiv](https://arxiv.org/html/2503.07376)
- SafeSwarm, arXiv 2501.07566, 2025: decentralized safe RL with barrier net; Crazyflie 2.1 + Vicon; 2.25 cm landing accuracy. — [arXiv](https://arxiv.org/abs/2501.07566)
- Motion-aware CBF flocking (IEEE journal, doc 11527353, 2025/2026): activates pairwise constraints only on collision risk to cut QP cost "with limited onboard computation"; Crazyflie experiments. — [IEEE Xplore](https://ieeexplore.ieee.org/document/11527353)
- Communication-free distributed navigation certified by field-of-view CBFs (MPC-CBF), arXiv 2502.01009: keeps neighbours in camera FOV for relative estimation; "robust to temporary tracking loss" — directly relevant to comm-denied flight. — [arXiv](https://arxiv.org/html/2502.01009)
- HMARL-CBF, NeurIPS 2025 (see Q1). — [NeurIPS PDF](https://papers.nips.cc/paper_files/paper/2025/file/76486c7eb6056f12e7ce3addced61650-Paper-Conference.pdf)
- Simulators: Crazyflow (JAX, differentiable), arXiv 2606.01478, 2026: "scales to millions of parallel environments and thousands of drones in a swarm, while maintaining a low sim-to-real gap"; notes CrazySwarm/CrazyChoir/Aerostack2 "lack native support for high-throughput batched simulation." — [arXiv](https://arxiv.org/html/2606.01478); CrazySim SITL (ICRA 2024) with decentralized MPC case study. — [Bitcraze blog](https://www.bitcraze.io/2024/04/crazysim-a-software-in-the-loop-simulator-for-the-crazyflie/)
- Earlier anchor: Batra et al., "Decentralized Control of Quadrotor Swarms with End-to-end Deep RL," CoRL 2021 — zero-shot transfer to real quadrotors. — [PMLR PDF](https://proceedings.mlr.press/v164/batra22a/batra22a.pdf)
- Decision-level sim-to-real: CATA/TACC used HIL training/validation and 10-UAV flight (Q3); LEARN six Crazyflies fully onboard (Q1).
- LLM-for-MRS survey reports that "prompts and plans are typically tuned against idealized simulator states with perfect localization, noise-free sensing," and field failures (wind-blown leaves on LiDAR, false positive detections, comm loss) "none of which surfaced in simulation." — [Li et al., Autonomous Robots 2026](https://link.springer.com/article/10.1007/s10514-026-10257-4)

### Inferences
- Maturity: safe low-level multi-agent control L2 (indoor, mocap localization); decision-level learned policies L2-L3 in only a handful of works; formal verification of learned swarm policies L1 or absent in sources found.
- Onboard: CBF-QP filters are lightweight and run on Crazyflie-class hardware when constraints are pruned (motion-aware activation); learned GCBF needs GNN inference per step, still small.
- Defense coverage: CDC partly (FOV-CBF communication-free navigation); CS/TA-A/HST largely untested with safety certificates; nearly all hardware results rely on Vicon/OptiTrack, i.e., GNSS-denied but *externally localized*, which is not GCL.
- Recurring methodological gap: safety guarantees are proven assuming perfect state knowledge of neighbours; coupling with estimation error from cooperative localization (Q5) is rarely treated.

### Gaps
- No 2024-2026 source on formal verification or runtime assurance (e.g., Simplex architecture) specifically for learned UAV-swarm policies was retrieved; this should be researched separately before claiming it is absent.
- Did not retrieve digital-twin-specific swarm sim-to-real papers with quantitative gap measurements.

---

## Q5. Differentiable / learned filtering and cooperative state estimation (learned Kalman filters, factor graphs, distributed SLAM, collaborative perception)

### Takeaway
Cooperative localization and C-SLAM are mature as model-based methods (distributed EKF/InEKF, factor graphs, Kimera-Multi/Swarm-SLAM lineage), and learned filters (KalmanNet family) have moved into distributed and federated forms in 2024-2025 — but almost exclusively for ground vehicles or 2-D simulations; learned cooperative estimation for GNSS-denied UAV swarms is barely touched. Multi-UAV collaborative perception has its own fast-growing feature-fusion literature, simulation/dataset-bound.

### Cited Findings
**Plain-words definition.** KalmanNet = keep the Kalman filter structure but let a small recurrent network learn the Kalman gain/noise statistics from data; distributed filters exchange only local estimates and covariances with neighbours; factor-graph C-SLAM = each robot's poses and inter-robot loop closures form a graph optimized jointly.

Learned / distributed filtering
- Revach, Shlezinger, Ni, López Escoriza, van Sloun, Eldar, "KalmanNet: Neural Network Aided Kalman Filtering for Partially Known Dynamics," *IEEE Trans. Signal Processing* 70:1532-1547, 2022, DOI 10.1109/tsp.2022.3158588 (anchor). — [cited in Piperigkos et al. record](https://exa.ai/library/publication/rvt9ndnpnwd)
- Piperigkos, Gkillas, Anagnostopoulos, Lalos, "Cooperative Plug-and-Play-KalmanNet for 4D situational awareness in autonomous driving," 2024 — KalmanNet as core of cooperative localization; CARLA simulation. — [Exa record](https://exa.ai/library/publication/rvt9ndnpnwd)
- FedKalmanNet, arXiv 2411.05847, 2024: federated adapt-then-combine training of KalmanNet across vehicles; outperforms collaborative decision-making that needs real-time V2X; CARLA only; future work on aggregation rules. Notes covariance-intersection CL methods "assume the true covariance matrices are known, without addressing how they can be estimated in practice." — [arXiv](https://arxiv.org/html/2411.05847)
- PFedKalmanNet-SA (Piperigkos et al.), 2026: cooperative localization in adaptive swarms of CAVs via joint distributed learning and decision-making. — [Exa record](https://exa.ai/library/publication/whn232y380s)
- NDKF (Neural-Enhanced Distributed Kalman Filter), arXiv 2502.02687, 2025: "most neural filtering approaches are applied in centralized settings"; extending to distributed partially observed MAS raises "ensuring stability despite learned-model bias, preventing overconfidence"; gives mean-square stability conditions and covariance-intersection fallback; validated only on a 2-D, 4-node simulation (~70%/41% error reduction vs distributed EKF). — [arXiv PDF](https://arxiv.org/pdf/2502.02687)
- DInEKF (Distributed Invariant EKF on matrix Lie groups), arXiv 2405.04000, 2024: fully distributed 3-D cooperative localization using one-hop neighbours; four Crazyflie 2.1 with IMU + UWB; better accuracy and NEES consistency than quaternion distributed EKF — but inter-robot relative measurements were *generated from mocap ground truth*. — [arXiv](https://arxiv.org/html/2405.04000)
- Review: "The development of distributed cooperative localization algorithms for Multi-UAV systems in the past decade," *Measurement* (Elsevier), 2025, S0263224125013995 (SJR Q1?, unverified): WoS query 2014-2025 returned 2,456 papers; centralized fusion vulnerable to "central node failure... cascading localization failures"; motivated by "electromagnetic interference or IMU drift." — [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0263224125013995)

Distributed / collaborative SLAM
- Review of distributed SLAM for multiple unmanned platforms (Chinese journal, Dec 2025): core challenges are "time synchronization, data association, and topological optimization"; existing datasets deficient in "heterogeneous system adaptability"; future: multimodal fusion and "lightweight map construction." — [chinasmp](http://tb.chinasmp.com/EN/Y2025/V0/I11/53)
- "A Survey on Collaborative SLAM with 3D Gaussian Splatting," arXiv 2510.23988, 2025: open challenges "lifelong mapping, semantic association and mapping, multi-model for robustness, and bridging the Sim2Real gap"; communication management and global consistency. — [arXiv](https://arxiv.org/html/2510.23988)
- Decentralized LiDAR multi-robot SLAM analysis, arXiv 2507.21553, 2025: loop detection is "the source of too many false positives" in underground tunnels. — [arXiv](https://arxiv.org/html/2507.21553v1)
- Multi S-Graphs, arXiv 2401.05152, 2024: distributed C-SLAM on hierarchical situational graphs minimizing data exchanged. — [arXiv PDF](https://arxiv.org/pdf/2401.05152)
- Lajoie et al., "Towards Collaborative SLAM: a Survey of the Current Research Landscape," arXiv 2108.08325 (baseline; robustness, communication, resource management as limits). — [arXiv PDF](https://arxiv.org/pdf/2108.08325)

Collaborative perception (multi-UAV)
- LIF ("Is Intermediate Fusion All You Need for UAV-based Collaborative Perception?"), arXiv 2504.21774, 2025: existing multi-UAV CP methods borrowed from driving "overlook the unique characteristics of the UAV perspective, resulting in substantial communication overhead"; shares compact detections + uncertainty-driven selection; 72.1% mAP / 61.4% NDS on UAV3D; "further consideration of localization errors will be a future direction." — [arXiv](https://arxiv.org/html/2504.21774v1)
- "A review of intelligent UAV swarm collaborative perception and computation," *Acta Aeronautica et Astronautica Sinica*, 2024, DOI 10.7527/S1000-6893.2024.30912 (Chinese). — [SciOpen](https://www.sciopen.com/article/10.7527/S1000-6893.2024.30912)
- CP datasets review (driving-centric), arXiv 2504.12696, 2025: most datasets use offline stitching and "lack modeling of real communication links, transmission latency"; CoPerception-UAV (NeurIPS 2022) is the main aerial dataset listed. — [arXiv](https://arxiv.org/html/2504.12696v1)
- STAMP (ICLR-track preprint arXiv 2501.18616): heterogeneous, model-agnostic CP via ~1 MB adapter-reverter pairs; notes CP "increased security vulnerabilities... compared to single-agent frameworks." — [arXiv](https://arxiv.org/html/2501.18616)
- Song, Xie, Wen, Li, "Wireless Communication as an Information Sensor for Multi-agent Cooperative Perception: A Survey," 2025 — techniques for "heterogeneity, localization errors, latency, and packet loss." — [Exa record](https://exa.ai/library/publication/fvkx8rlyq5r)

### Inferences
- Maturity: model-based distributed CL/C-SLAM L2-L3; learned filters (KalmanNet family) L1 for multi-agent use, and the multi-agent variants found are vehicle/2-D; UAV collaborative perception L1 (simulated datasets UAV3D, CoPerception-UAV).
- Onboard: KalmanNet-style gain networks are small (designed for low complexity); CP intermediate-fusion BEV features are bandwidth-heavy, which motivates late/late-intermediate fusion for UAVs.
- Defense coverage: GCL has a large model-based literature but little learned/differentiable estimation for swarms under jamming; CP for drones exists but ignores localization error and adversarial/spoofed shared features in the sources found; coupling of estimation with MARL/CBF (Q1, Q4) is rarely done (Active-SLAM survey frames it as coupled Dec-POMDP + factor graph).
- Methodological gap: learned estimators lack consistency (NEES) guarantees in distributed fusion; NDKF explicitly lists overconfidence under learned-model bias as open.

### Gaps
- No 2024-2026 paper found applying KalmanNet-type learned filters to real multi-UAV cooperative localization (UWB/vision ranging) in GNSS-denied flight.
- Did not retrieve Kimera-Multi / Swarm-SLAM / D2SLAM primary papers in this session; their status is from background knowledge and not cited here.

---

## Q6. LLM / VLM-based mission planning, human-swarm interfaces, small LLMs on edge devices, agentic frameworks, and reliability

### Takeaway
LLMs are being used as high-level planners/translators over a library of RL-trained or classical primitives (TALKER, COHERENT), and small quantized VLMs/LLMs now run onboard Jetson-class UAVs with sub-second (2B VLM) to 8-10 s (1.1B on Jetson Nano) latency; but surveys converge that hallucination, numerical-reasoning fragility, latency/connectivity, lack of benchmarks for hallucination/latency, and sim-tuned prompts make them unreliable for deployment, especially under lossy communication.

### Cited Findings
**Plain-words definition.** The LLM converts natural-language mission intent into structured plans/code that call pre-built skills (fly-to, search, track); a VLM grounds words in camera images; "agentic" frameworks loop plan → execute → feedback → re-plan.

Surveys and reliability
- Li, An, Abrar, Zhou, "Large language models for multi-robot systems: a survey," *Autonomous Robots* 50, art. 30, 2026, DOI 10.1007/s10514-026-10257-4 (SJR Q1?, unverified): challenges = "mathematical reasoning limitations, hallucination, latency issues, and the need for robust benchmarking"; performance drops "up to 65%" when irrelevant clauses are added; none of four reviewed benchmarks report "hallucination rate, token consumption, API-call count, wall-clock inference latency... or robustness to perception noise"; "deployment-grade robustness in the face of latency variance, lossy communication, and accumulated multi-robot uncertainty remains largely unaddressed"; only Cladera et al. 2025 and Ravichandran et al. 2025 designed for intermittent communication; server-based LLMs make remote field deployment "unachievable." — [Springer](https://link.springer.com/article/10.1007/s10514-026-10257-4); [arXiv v5](https://arxiv.org/html/2502.03814v5)
- "Large Language Model-Assisted UAV Operations and Communications: A Multifaceted Survey and Tutorial," arXiv 2602.19534, 2026 (preprint): MLLM human-swarm interaction work cites "hallucinations, inference latency, and communication bottlenecks"; one cited system reached "up to 91.7% accuracy and an average response time of 5.7 seconds"; calls for agent frameworks with verifiable subtasks, automated validators, guardrails, HITL checkpoints. — [arXiv](https://arxiv.org/html/2602.19534v2)
- Tian et al., "UAVs Meet LLMs: Overviews and Perspectives Toward Agentic Low-Altitude Mobility," arXiv 2501.02341, 2025 (paper list incl. TypeFly, REAL, AutoHMA-LLM). — [GitHub](https://github.com/Hub-Tian/UAVs_Meet_LLMs)
- Basak et al., "Aerial mirage: unmasking hallucinations in large vision language models," WACV 2025 (aerial-image VLM hallucination). — [cited in arXiv 2602.19534](https://arxiv.org/html/2602.19534v2)

Swarm-specific LLM methods
- **TALKER** — Lou, Shi, Lin, Wang, Wu, "TALKER: A Task-Activated Language Model Based Knowledge-Extension Reasoning System," *IEEE Robotics and Automation Letters*, online 4 Dec 2024 (listed as RA-L 2025) (SJR Q1?, unverified): MARL-trained fine-grained drone skills → action primitive library; LLM plans with these primitives, refined by user feedback; successful task code stored ("knowledge expansion"); tasks: collaborative search, object tracking, cooperative interception, aerial patrol. — [Exa record](https://exa.ai/library/publication/q52r3m6p5ps); [aiconfpaper](https://aiconfpaper.com/paper/ral-2025-LouSLWW25)
- COHERENT (arXiv 2409.15146): Proposal-Execution-Feedback-Adjustment loop for heterogeneous quadrotor/dog/arm teams; 100-task benchmark. — [arXiv](https://arxiv.org/html/2409.15146v3)
- REBEL (arXiv 2409.16266): LLM + RAG initial task allocation in multi-human multi-robot teams, complementing RL allocators. — [arXiv](https://arxiv.org/html/2409.16266v1)
- SwarmChain: Collaborative LLM Inference for UAV Swarm Control, *IEEE Internet of Things Magazine* 8(5):64-71, 2025, DOI 10.1109/miot.2025.3575886; SwarmChat (Eumi, Abbass, Marcus), LNCS 2025 — LLM multimodal human-swarm interaction. — [listed in references of Exa record](https://exa.ai/library/publication/nd1r0tqxhzr)

Edge / onboard evidence
- VLN on the Fly (GitHub project, 2026): INT4 Qwen-3.5-2B VLM on Jetson Orin NX, median 0.79 s total inference (95th pct 0.88 s), 13/15 real flights successful; grounding to a 3x3 grid cell instead of pixels; finite-state-machine safety gate; still uses OptiTrack for pose. — [GitHub](https://github.com/peDrontonio/VLNontheFly)
- ATLASv2 (Walczak, Kallakuri, Mohsenin), arXiv 2504.10784, 2025: TinyLLaMA 1.1B Q5 (745 MB) on Jetson Nano 4 GB; onboard plan latency 8-10 s vs ~20 ms cloud; power spikes to 9.2 W; RAM ~92% (ground robot). — [alphaXiv](https://www.alphaxiv.org/abs/2504.10784)
- PX4 + ROS 2 + Ollama agentic drone framework (Lim et al.), arXiv 2506.07509, 2025: benchmarked Gemma3-4B, Qwen2.5-3B, Llama3.2-3B, DeepSeek-7B and VLMs (7-12B) on a Jetson Orin Nano quadcopter; authors call for "smaller, edge-deployable models with fewer than one billion parameters." — [alphaXiv](https://www.alphaxiv.org/abs/2506.07509)
- Onboard 14B LLM UAV (arXiv 2503.08302, 2025): 5-6 tokens/s at ~220 W peak on a 10-15 kg hexacopter — shows the size/power cost of large onboard models. — [arXiv PDF](https://export.arxiv.org/pdf/2503.08302)
- Seymour, Kütükçü, Baidya, "Large Language Models on Small Resource-Constrained Systems: Performance Analysis and Trade-Offs," 2025: baseline characterization of Pythia 70M-1.4B on Jetson Orin. — [Exa record](https://exa.ai/library/publication/q9bkktsqmpn)
- Narasimhamurthy et al., "Real-Time UAV Swarm Autonomy Using Edge-Deployed Small Language Models," 2026 (video demonstration; Jetson Orin Nano; venue unclear). — [Exa record](https://exa.ai/library/publication/nd1r0tqxhzr)

### Inferences
- Maturity: LLM-over-primitives planning L1-L2 (TALKER simulation/hardware status not stated in retrieved abstract); onboard VLM grounding for single UAV L3 indoor; swarm-level onboard LLM coordination L1-L2.
- Onboard: ≤2-4B quantized models fit Jetson Orin NX/Nano with ~1 s (VLM grounding) to ~10 s (planning) latency; this confines LLMs to the slow deliberative layer, with RL/CBF layers handling real-time control.
- Defense coverage: HST is the primary application; CS appears only as "cooperative interception" in TALKER; CDC is the most explicit unaddressed condition (survey: lossy communication "largely unaddressed"); TA-A via LLM allocators (REBEL, COHERENT) lacks attrition tests; prompt-injection from adversarial data sources flagged as risk.
- Methodological gap: no shared metrics for hallucination/latency/re-planning frequency in multi-robot LLM benchmarks; verification of LLM outputs (formal checks, validators) proposed but not systematically evaluated.

### Gaps
- Did not find a peer-reviewed 2024-2026 study measuring LLM plan error rates for a real multi-UAV swarm under degraded communication.
- Could not confirm whether TALKER included real-drone experiments.

---

## Q7. Game-theoretic and adversarial learning (self-play) for pursuit-evasion / counter-swarm

### Takeaway
Swarm confrontation is one of the most active MARL application areas (especially in Chinese aerospace journals and IEEE TAES), using self-play, staged/curriculum opponents, attention for scale and hierarchical macro-actions; but results are almost entirely simulation-based with hand-designed opponents, and a 2025 review explicitly notes differential games do not scale while MARL lacks stability and interpretability.

### Cited Findings
**Plain-words definition.** Self-play = the policy is trained against copies (or a growing population) of itself so that the opponent improves as training proceeds; differential-game methods compute equilibrium strategies analytically from dynamics.

- Xu, "New Explorations in Autonomous Low-Altitude Area Defense Decision-Making and Control Methods of UAV Swarms," *Guidance, Navigation and Control*, 2025, DOI 10.1142/S2737480725030013: categorizes approaches into differential games, MARL, bio-inspired; "traditional differential games struggle with scalability and MARL approaches face stability and interpretability issues"; open challenges: mapping biological behaviours to UAV rules, modelling maneuverability with environmental constraints, "inferring intent for mission planning"; calls for "formal control guarantees" for many-vs-many defense. — [World Scientific](https://www.worldscientific.com/doi/10.1142/S2737480725030013)
- AMAAC (IEEE TAES 2025): self-play-based extended training generalizes from small to larger confrontations (see Q1). — [Exa record](https://exa.ai/library/publication/7vd5ck2yjjb)
- MARL-LAC, "Multi-agent reinforcement learning with layered autonomy and collaboration for enhanced collaborative confrontation," *Chinese Journal of Aeronautics*, 2025, DOI 10.1016/j.cja.2025.103747: dual twin critics; global swarm reward + local defender rewards; notes current algorithms "sensitive to fluctuations in enemy strategies... especially when rewards are sparse." — [SciOpen](https://www.sciopen.com/article/10.1016/j.cja.2025.103747)
- MSRM-MAPOCA, *Actuators* 14(1):15, 2025, DOI 10.3390/act14010015: heterogeneous teams (quantity vs resilience advantage); staged training — semi-static opponent then self-play; macro-state rewards against sparse reward; Unity simulation (UGVs). Related-work section lists scenario-transfer and self-play training, inverse-RL reward recovery, bio-inspired hunting. — [MDPI](https://www.mdpi.com/2076-0825/14/1/15)
- Su, Hou, Hong, "Heterogeneous Policy Network Reinforcement Learning for UAV Swarm Confrontation," 2024: heterogeneous policy networks with local parameter sharing inside MAPPO for reconnaissance-attack swarms (simulation). — [ResearchGate](https://www.researchgate.net/publication/388984171_Heterogeneous_Policy_Network_Reinforcement_Learning_for_UAV_Swarm_Confrontation)
- APIQ (attention + value decomposition) for multi-UAV attack-defense, *Systems Engineering and Electronics* 47(7), 2025. — [sys-ele](https://www.sys-ele.com/EN/10.12305/j.issn.1001-506X.2025.07.14)
- Bio-inspired grouping MARL for attack-defense, *Biomimetics* 8(2):222, 2023: training time "increases exponentially as the swarm size increases"; trains 4-UAV groups and composes to 12 UAVs; >91% interception when enemy acceleration ≤2.5x. — [MDPI](https://www.mdpi.com/2313-7673/8/2/222)
- Hierarchical HMM-intent + QMIX defense (SJTU journal 2025) — intent recognition layer improves win rate (see Q1). — [SJTU](https://www.qk.sjtu.edu.cn/ktfy/EN/abstract/abstract50436.shtml)
- MRS Group (CTU Prague) demonstrates fast evasion of self-localized UAV swarms from an intruder (real flights). — [MRS group page](https://mrs.fel.cvut.cz/research/swarm-robotics)

### Inferences
- Maturity: L1 for learned counter-swarm policies (Unity/Python/MAgent simulators); evasion behaviours with classical control reach L3 (CTU).
- Onboard: execution policies are small; the open issue is opponent-model generalization, not compute.
- Methodological gaps triangulated: (i) evaluation against fixed or self-generated opponents only — no population-based/league training or exploitability measurement reported in the UAV papers found; (ii) little coupling with communication denial (opponent jamming) or attrition-aware re-tasking; (iii) no safety certificates in adversarial settings; (iv) intent inference flagged as open by Xu (2025).
- Defense coverage: CS is the core; CDC and GCL rarely combined with confrontation; HST absent.

### Gaps
- Did not retrieve a 2024-2026 paper computing Nash-equilibrium exploitability (e.g., PSRO-style) for UAV swarm confrontation; absence not confirmed.
- Did not retrieve 2024-2026 differential-game pursuit-evasion journal papers with learning hybrids (e.g., in IEEE TAES / Automatica).

---

## Q8. Federated and decentralized learning across swarms

### Takeaway
Federated learning for UAV swarms is a communications-community topic (scheduling, power, asynchronous aggregation, multi-hop) with mainly simulation results; asynchronous and server-less (gossip/leader) variants address unstable links, but onboard training cost, Byzantine robustness and federated *control/RL* policies (vs. perception models) remain underexplored in the sources found.

### Cited Findings
**Plain-words definition.** Each UAV trains a model on its own data; only model weights/updates (not raw data) are exchanged and averaged, either through a leader/ground server or peer-to-peer.

- "Distributed Machine Learning for UAV Swarms: Computing, Sensing, and Semantics," *IEEE Internet of Things Journal* 11(5), 2024, doc 10353003 (SJR Q1?, unverified): covers FL, MARL, distributed inference, split learning for swarms; lists open problems (not retrieved in detail). — [IEEE Xplore](https://ieeexplore.ieee.org/document/10353003)
- Cui, Yang, Wu, Feng, Hu, "The Data Value Based Asynchronous Federated Learning for UAV Swarm Under Unstable Communication Scenarios," *IEEE Trans. Mobile Computing* 23(6):7165-7179, 2024, DOI 10.1109/TMC.2023.3331906 (SJR Q1?, unverified): synchronous aggregation "no longer tenable" in swarms; Shapley-value data valuation; "Network Age of Updates" scheduling via Whittle index; theory + simulation. — [ACM DL](https://dl.acm.org/doi/10.1109/TMC.2023.3331906)
- Delay- and overhead-efficient FL transmission scheduling in multi-hop UAV swarms, arXiv 2405.00681, 2024: proves minimal delay/overhead with BFS-tree aggregation; up to 71% and 96% less traffic vs shortest-path and prior scheme at 400 UAVs; future work on topology variation. — [arXiv](https://arxiv.org/html/2405.00681)
- Zeng et al., "Federated Learning in the Sky: Joint Power Allocation and Scheduling with UAV Swarms" (ICC 2020 / arXiv 2002.08196): leader-follower FL; up to 35% fewer rounds (anchor). — [NSF PAR PDF](https://par.nsf.gov/servlets/purl/10143996)
- Najafinia, Wang, Lai, "More Than a Mobile Client: A Systematic Literature Review of Architectures, Applications, and Challenges of UAV-Enabled Federated Learning," 2026. — [Exa record](https://exa.ai/library/publication/0ss3wp03t4r)
- UAV-assisted energy-efficient edge FL survey, *Computer Science* (China) 51(4), 2024: challenges "limited communication bandwidth, unreliable communication environment, and uncertainty of flight environment." — [jsjkx](https://www.jsjkx.com/EN/10.11896/jsjkx.231100084)
- Ekechi et al. (Drones 2025) devote a section to "Multi-agent Federated Reinforcement Learning Techniques" for UAV control. — [MDPI](https://www.mdpi.com/2504-446X/9/7/484)
- FedKalmanNet (Q5) shows FL of learned filters for cooperative localization (vehicles). — [arXiv](https://arxiv.org/html/2411.05847)

### Inferences
- Maturity: L1 (simulation/theory) for swarm FL; no flight-validated swarm FL found.
- Onboard: inference is feasible; on-board *training* on Jetson-class or smaller hardware with flight-energy budgets is not characterized in the sources found.
- Defense coverage: CDC partially (asynchronous, multi-hop, unstable links); poisoning/Byzantine attacks by compromised swarm members not addressed in UAV-FL sources retrieved; GCL via FedKalmanNet only for cars; TA-A/CS/HST absent.

### Gaps
- Did not retrieve open-problem sections of the IoT-J 2024 survey or the 2026 SLR.
- No source found on federated MARL policy training validated on real UAVs.

---

## Cross-cutting synthesis (method x defense problem coverage, from sources above)

### Takeaway
Across all families, the commonest methodological pattern is "learned component inside a classical, guaranteed scaffold" (learned gating over CBBA, learned CBF certificates, LLM over RL primitives, KalmanNet inside EKF). Open gaps cluster at the junctions: guarantees lost when learned parts are inserted, estimation error ignored by planners/safety filters, and attrition/adversarial communication rarely modelled jointly.

### Cited Findings
- Hybrid-scaffold examples: CATA/TACC learned gating + auction ([TAES](https://exa.ai/library/publication/h8s6crq0fw9)); learned CBBA bidder ([arXiv 2605.21932](https://arxiv.org/html/2605.21932)); GCBF+ ([arXiv](https://arxiv.org/html/2401.14554v4)); TALKER ([RA-L](https://exa.ai/library/publication/q52r3m6p5ps)); NDKF ([arXiv](https://arxiv.org/pdf/2502.02687)).
- Real-hardware anchors 2024-2026: 10 fixed-wing UAVs (TACC/CATA); six Crazyflies fully onboard (LEARN); Crazyflie swarms with mocap (GCBF+, Layered Safe MARL, AttentionSwarm, SafeSwarm, DInEKF); single UAV onboard VLM 0.79 s (VLN on the Fly).

### Inferences
Coverage matrix (S = studied in sim, H = hardware evidence found, – = not found in this session):

| Method family | TA-A | CDC | CS | CP | GCL | HST |
|---|---|---|---|---|---|---|
| MARL (CTDE/attention/mean-field/HRL) | S (agent death in GPMF) | S | S (many) | – | – | – |
| GNN / learned communication | – | S, H (via CATA) | – | S (feature sharing) | – | – |
| Auction/CBBA + learning | S (CBPA capability loss) | S, H (CATA/TACC) | S | – | – | S (I-CBBA) |
| Sim-to-real / safe RL / CBF | – | S (FOV-CBF) | – | – | – (mocap used) | – |
| Learned filtering / C-SLAM / CP | – | S | – | S (UAV3D) | S, H model-based; learned only for cars | – |
| LLM / VLM | S (allocators) | – (flagged open) | S (interception in TALKER) | – | – | S, H (single UAV) |
| Game-theoretic / self-play | – | – | S | – | – | – |
| Federated / decentralized learning | – | S (async FL) | – | – | S (cars) | – |

- The "–" cells indicate absence *in the sources retrieved here*, not proven absence in the literature.

### Gaps
- Scimago/WoS quartiles for all venues remain unverified in this session.
- Topics not adequately covered due to search budget: formal verification/runtime assurance for learned swarm policies; digital-twin swarm sim-to-real quantification; primary C-SLAM systems (Kimera-Multi, Swarm-SLAM, D2SLAM); league/PSRO training for counter-swarm; Byzantine-robust swarm FL.
