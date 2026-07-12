# Agentic Robotics Reading List

A curated, ordered path through the line of work that goes from **language-conditioned control** to **autonomous physical research** - what I've been calling *agentic robotics*.

The through-line to keep in mind while reading: **"What does this paper hand off from humans to AI?"** The answer marches forward each stage - planning → policy code → rewards → skill accumulation → the entire research loop.

**Read deeply (the hinge papers):** Code as Policies, Eureka, Voyager, ASPIRE, ENPIRE. Skim the rest for abstract + method figure + results table.

---

## Stage 1 - Foundations: LLMs first meet robots (2022)

1. [**SayCan** - Do As I Can, Not As I Say: Grounding Language in Robotic Affordances](https://arxiv.org/abs/2204.01691) · Ahn et al., Google, 2022
   High-level LLM planning + a value function for feasibility scoring. Read it to understand how the *grounding problem* was first framed.
2. [**Socratic Models** - Composing Zero-Shot Multimodal Reasoning with Language](https://arxiv.org/abs/2204.00598) · Zeng et al., Google, 2022
   Multiple foundation models collaborating through language. The intellectual seedbed for Code as Policies.
3. [**Code as Policies** - Language Model Programs for Embodied Control](https://arxiv.org/abs/2209.07753) · Liang et al., Google, 2022 — **read deeply**
   The core paper: represent the *policy itself* as LLM-generated code.
4. [**ProgPrompt** - Generating Situated Robot Task Plans using LLMs](https://arxiv.org/abs/2209.11302) · Singh et al., NVIDIA/USC, 2022
   Parallel work to CaP; programmatic prompting for task plans. Reading it alongside CaP shows the design space.
5. [**Inner Monologue** - Embodied Reasoning through Planning with Language Models](https://arxiv.org/abs/2207.05608) · Huang et al., Google, 2022 · [project](https://innermonologue.github.io/)
   Introduces closed-loop feedback - environment feedback fed back to the LLM as language. The prototype for all later "autonomous debug" loops.

## Stage 2 - Extending the code interface (2023)

6. [**VoxPoser** - Composable 3D Value Maps for Robotic Manipulation with Language Models](https://arxiv.org/abs/2307.05973) · Huang et al., Stanford, 2023
   Code writes 3D value maps instead of calling fixed action primitives.
7. [**Language to Rewards** - for Robotic Skill Synthesis](https://arxiv.org/abs/2306.08647) · Yu et al., Google DeepMind, 2023
   LLM writes reward functions feeding an MPC controller. The prelude to Eureka.
8. [**Eureka** - Human-Level Reward Design via Coding LLMs](https://arxiv.org/abs/2310.12931) · Ma et al., NVIDIA, 2023 — **read deeply**
   LLM + evolutionary search to write reward functions. The "LLM as optimizer" paradigm.
9. [**Text2Reward** - Reward Shaping with Language Models for RL](https://arxiv.org/abs/2309.11489) · Xie et al., 2023
   Parallel work to Eureka; good to contrast.

## Stage 3 - Agents, skill libraries, and lifelong learning

10. [**Voyager** - An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) · Wang et al., NVIDIA, 2023 — **read deeply**
    In Minecraft, but it's the prototype of "coding agent + automatic curriculum + skill library" - the direct ancestor of ASPIRE.
11. [**RoboGen** - Unleashing Infinite Data for Automated Robot Learning via Generative Simulation](https://arxiv.org/abs/2311.01455) · Wang et al., CMU, 2023
    Agent auto-generates tasks, scenes, and training supervision - the "generative simulation" route.
12. [**DrEureka** - Language Model Guided Sim-To-Real Transfer](https://arxiv.org/abs/2406.01967) · Ma et al., 2024
    Extends Eureka to sim-to-real; LLM automates domain randomization.

## Stage 4 - The control group: VLA and world-model routes

To locate agentic robotics, you have to understand its competing routes.

13. [**RT-2** - Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://arxiv.org/abs/2307.15818) · Google DeepMind, 2023
    Establishes the VLA concept.
14. Modern VLA representatives (π0 is the more worthwhile read):
    - [**OpenVLA** - An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246) · Kim et al., Stanford/Berkeley, 2024
    - [**π0** - A Vision-Language-Action Flow Model for General Robot Control](https://arxiv.org/abs/2410.24164) · Physical Intelligence, 2024
15. World-model route (skim for the tension between the three routes):
    - [**DreamerV3** - Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104) · Hafner et al., Google DeepMind, 2023
    - [**Genie** - Generative Interactive Environments](https://arxiv.org/abs/2402.15391) · Bruce et al., Google DeepMind, 2024
    - [**UniSim** - Learning Interactive Real-World Simulators](https://arxiv.org/abs/2310.06114) · Yang et al., Berkeley/Google DeepMind, 2023

## Stage 5 - The methodology of autonomous AI research (not robotics, but essential)

16. [**FunSearch** - Mathematical discoveries from program search with large language models](https://www.nature.com/articles/s41586-023-06924-6) · Google DeepMind, Nature, 2023 · [blog](https://deepmind.google/blog/funsearch-making-new-discoveries-in-mathematical-sciences-using-large-language-models/)
    LLM + evolutionary search discovering new math. The methodological origin of "searching program space."
17. [**AlphaEvolve** - A coding agent for scientific and algorithmic discovery](https://arxiv.org/abs/2506.13131) · Novikov et al., Google DeepMind, 2025 · [announcement](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)
    FunSearch scaled up - evolutionary code optimization.
18. [**The AI Scientist** - Towards Fully Automated Open-Ended Scientific Discovery](https://arxiv.org/abs/2408.06292) · Lu et al., Sakana AI, 2024
    The first complete attempt at end-to-end automated research - the digital-world prototype of "autoresearch."

## Stage 6 - Physical Autoresearch (2026, frontier)

19. [**ASPIRE** - Agentic Skills Discovery for Robotics](https://arxiv.org/abs/2607.00272) · Lu, Wu, Kou et al. (incl. Goldberg, Zhu, Fan, Wang), NVIDIA GEAR + Michigan/UIUC/Berkeley/CMU, 2026 · [project](https://research.nvidia.com/labs/gear/aspire/) — **read deeply**
    Closed-loop execution engine + skill library + evolutionary search. Robot writes code → runs → fails → self-diagnoses from multimodal traces → distills fixes into a reusable skill library.
20. [**ENPIRE** - Agentic Robot Policy Self-Improvement in the Real World](https://arxiv.org/abs/2606.19980) · Xiao, Xie et al. (incl. Goldberg, Fan, Zhu, Shi), NVIDIA GEAR + CMU + Berkeley, 2026 · [project](https://research.nvidia.com/labs/gear/enpire/) — **read deeply**
    Formalizes *physical autoresearch*. Four modules: **En**vironment / **P**olicy Improvement / **R**ollout / **E**volution. Coding agents run the full research loop on real hardware; introduces multi-robot scaling laws.

---

### Reading strategy

- Deep-read the five hinge papers (CaP, Eureka, Voyager, ASPIRE, ENPIRE); skim the rest (abstract + method figure + results table).
- Every deep-read paper's *related work* section is itself a good map - ENPIRE's citation list in particular covers most of this field.
- Carry the question "what got handed from humans to AI?" through all six stages. The progression - planning → policy code → rewards → skill accumulation → the whole research loop - *is* the definition of agentic robotics.

### Notes on sources

- All links verified to resolve to the correct paper (arXiv abstract pages, or Nature / project pages where more canonical).
- **ASPIRE (#19)** and **ENPIRE (#20)** are very recent (June/July 2026) NVIDIA GEAR papers; titles here are the official ones (some earlier informal descriptions used different backronym expansions). Verified via arXiv + NVIDIA GEAR project pages.
- FunSearch has no standalone arXiv page - the Nature article is the canonical link.

---

*Reading list assembled from a conversation tracing the agentic-robotics lineage. Inspired in format by [jrin771/Frontier_Robotics_Reading_List](https://github.com/jrin771/Frontier_Robotics_Reading_List).*
