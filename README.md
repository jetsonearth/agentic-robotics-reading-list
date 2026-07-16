# Agentic robotics reading list

An ordered path from **language-conditioned control** to **autonomous physical research** - what I call *agentic robotics*.

Agents have mostly lived in the screen: chatbots, tool callers, coding agents that edit repos while you sleep. The next step is physical AI - bringing those same loops onto robots that act in the world, fail, notice, and try again. This list is the paper trail I followed when I got hooked on that idea (via NVIDIA's ENPIRE / physical autoresearch work, then backward to Eureka and Code as Policies).

**Question to carry through every paper:** *What did this hand off from humans to AI?*

Rough progression:

| Stage | What gets automated |
|-------|---------------------|
| 0 | Think-act loops in software |
| 1 | Language → robot plans / code |
| 2 | Language → rewards, then RL |
| 3 | Skills that accumulate over time |
| 4 | (Side paths: VLAs, world models) |
| 5 | Digital "do the research yourself" |
| 6 | Same research loop on real robots |

Order is by *capability*, not calendar. Eureka and FunSearch landed in the same season; Voyager is earlier than both. Don't treat the stages as a strict timeline.

**Read deeply (hinges):** Code as Policies, Eureka, Voyager, ASPIRE, ENPIRE.  
**Skim the rest:** abstract + method figure + results table is enough.

---

## Before you treat any of this as solved

"Self-programming robots" is real work and also easy to oversell. A few limits that still hold after ASPIRE and ENPIRE:

1. **Frozen interfaces.** ASPIRE (and most CaP-style systems) debug *inside* a fixed perception / planning / control API. The agent rewrites task code, not the whole stack. ASPIRE's own limitations section is clear about this.
2. **Humans still build the harness.** ENPIRE needs auto-reset, auto-verify, logging, and safety before coding agents can run unsupervised trials. That harness is a lot of the product. Physical autoresearch does not mean "drop Claude on a random arm and walk away."
3. **Search, not unbounded invention.** Today's self-improvement is mostly search in *program space* or *reward space* under a human-designed interface - propose candidates, run them, keep winners. That is powerful. It is not the robot inventing new physics or new embodiment from nothing.
4. **Safety and success detection are still hard.** Real-world loops need reliable reset, stop conditions, and honest evaluation. When papers report high success rates, read the metric (e.g. ENPIRE's pass@8 is in-context retries inside a long-horizon loop, not naive best-of-8 sampling).
5. **Digital and physical are the same pattern, different cost.** Tokens are cheap; robot hours and broken hardware are not. That is why harness design matters as much as the LLM.

Keep those in mind so the list reads as a research path, not a victory lap.

---

## Stage 0 - Digital agent loops (the pattern before the body)

Physical autoresearch is not a brand-new idea. It is the embodied version of loops software people already know: reason, act with tools, observe, revise.

0. [**ReAct** - Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) · Yao et al., 2022  
   Interleave reasoning traces with tool/environment actions. The basic "think, call something, look, think again" skeleton that later robot agents still use.

1. [**Reflexion** - Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) · Shinn et al., 2023  
   After failure, write a short linguistic self-critique into memory and try again - no weight updates. Prototype for "debug in language, not in gradients."

**Also in this family (no need to deep-read for the robotics arc):** tool-using coding agents that edit real repos - Claude Code, Codex, SWE-agent-style systems. Same loop: propose code → run tests / tools → read logs → patch. ENPIRE is roughly that loop with a robot farm instead of a CI runner.

---

## Stage 1 - LLMs first meet robots (2022)

2. [**SayCan** - Do As I Can, Not As I Say: Grounding Language in Robotic Affordances](https://arxiv.org/abs/2204.01691) · Ahn et al., Google, 2022  
   LLM proposes skills; a value/affordance model scores what is actually feasible on the robot. Classic framing of the *grounding* problem: language is cheap, physics is not.

3. [**Socratic Models** - Composing Zero-Shot Multimodal Reasoning with Language](https://arxiv.org/abs/2204.00598) · Zeng et al., Google, 2022  
   Several foundation models talking to each other through language. Same circle of people as Code as Policies; useful context for why "everything as text/code" felt natural.

4. [**Code as Policies** - Language Model Programs for Embodied Control](https://arxiv.org/abs/2209.07753) · Liang et al., Google, 2022 · **read deeply**  
   The hinge: the *policy itself* is LLM-generated code (language model programs), not just a plan over fixed skills. If you only deep-read one 2022 paper, make it this one.

5. [**ProgPrompt** - Generating Situated Robot Task Plans using LLMs](https://arxiv.org/abs/2209.11302) · Singh et al., NVIDIA / USC, 2022  
   Parallel to CaP: programmatic prompts for task plans. Read next to CaP to see the design space (plan-as-code vs policy-as-code).

6. [**Inner Monologue** - Embodied Reasoning through Planning with Language Models](https://arxiv.org/abs/2207.05608) · Huang et al., Google, 2022 · [project](https://innermonologue.github.io/)  
   Closed loop: environment feedback comes back to the LLM as language. Early template for later "run, fail, narrate, repair" systems.

---

## Stage 2 - Code writes more than motion (2023-2024)

Once code is the interface, people start generating denser objects than "pick up the cup."

7. [**VoxPoser** - Composable 3D Value Maps for Robotic Manipulation with Language Models](https://arxiv.org/abs/2307.05973) · Huang et al., Stanford, 2023  
   LLM/code builds 3D value maps for motion, not only sequences of named primitives.

8. [**Language to Rewards** - for Robotic Skill Synthesis](https://arxiv.org/abs/2306.08647) · Yu et al., Google DeepMind, 2023  
   LLM writes reward functions for an MPC stack. Direct setup for Eureka-style work: language shapes the objective, optimizer or RL does the rest.

9. [**Eureka** - Human-Level Reward Design via Coding LLMs](https://arxiv.org/abs/2310.12931) · Ma et al., NVIDIA, 2023 · **read deeply**  
   LLM proposes reward *code*; evolutionary search keeps variants that train better policies. Think "LLM as reward engineer," not a generic optimizer. Huge step: humans stop hand-writing rewards for every skill.

10. [**Text2Reward** - Reward Shaping with Language Models for RL](https://arxiv.org/abs/2309.11489) · Xie et al., 2023  
    Concurrent with Eureka. Useful contrast paper if you care about the design choices.

11. [**DrEureka** - Language Model Guided Sim-To-Real Transfer](https://arxiv.org/abs/2406.01967) · Ma et al., 2024  
    Eureka-family follow-up: LLM also helps domain randomization / sim-to-real, not only the reward.

---

## Stage 3 - Open-ended agents and skill libraries

12. [**Voyager** - An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) · Wang et al., NVIDIA, 2023 · **read deeply**  
    Minecraft, not a robot arm - still the cleanest early demo of *coding agent + automatic curriculum + skill library*. Pattern ancestor of ASPIRE (shared people and ideas; different world). Skills compound; the agent does not start from zero every task.

13. [**RoboGen** - Unleashing Infinite Data for Automated Robot Learning via Generative Simulation](https://arxiv.org/abs/2311.01455) · Wang et al., CMU, 2023  
    Agent proposes tasks, scenes, and training supervision in simulation. Another route to "keep generating work for yourself" without a human curriculum designer on every trial.

---

## Stage 4 - Other routes: VLAs and world models

Agentic robotics is one bet. Two others dominate the industry conversation. You need them as context so "agentic" does not sound like the only possible future - and so you can argue for composition (agents on top of VLAs / world models) instead of pure rivalry.

14. [**RT-2** - Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://arxiv.org/abs/2307.15818) · Google DeepMind, 2023  
    Canonical early VLA: web-scale vision-language knowledge into robot actions.

15. Later VLA samples (π0 is the better single read if you pick one):
    - [**OpenVLA** - An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246) · Kim et al., Stanford / Berkeley, 2024
    - [**π0** - A Vision-Language-Action Flow Model for General Robot Control](https://arxiv.org/abs/2410.24164) · Physical Intelligence, 2024

16. World-model samples (skim for the third pole of the triangle):
    - [**DreamerV3** - Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104) · Hafner et al., Google DeepMind, 2023
    - [**Genie** - Generative Interactive Environments](https://arxiv.org/abs/2402.15391) · Bruce et al., Google DeepMind, 2024
    - [**UniSim** - Learning Interactive Real-World Simulators](https://arxiv.org/abs/2310.06114) · Yang et al., Berkeley / Google DeepMind, 2023

Rough triangle: **VLA** = end-to-end policy from data; **world model** = learn dynamics then plan or imagine; **agentic / code** = LLM (or coding agent) searches programs, rewards, or research steps under tools and feedback.

---

## Stage 5 - Digital autoresearch (not robotics, still essential)

Same idea class as Eureka-style search, pointed at math, algorithms, and full paper-writing loops. These are not "ancestors" of Eureka in a strict timeline - Eureka (Oct 2023) and FunSearch (late 2023) are closer to siblings - but they make the *methodology* obvious before you put it on hardware.

17. [**FunSearch** - Mathematical discoveries from program search with large language models](https://www.nature.com/articles/s41586-023-06924-6) · Google DeepMind, Nature, 2023 · [blog](https://deepmind.google/blog/funsearch-making-new-discoveries-in-mathematical-sciences-using-large-language-models/)  
    LLM proposes programs; evolutionary search keeps the ones that score well on a task. Clean digital example of "search program space with an LLM proposal distribution." (Program search itself is much older; this is the modern LLM flavor.)

18. [**AlphaEvolve** - A coding agent for scientific and algorithmic discovery](https://arxiv.org/abs/2506.13131) · Novikov et al., Google DeepMind, 2025 · [announcement](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)  
    FunSearch-scale ambition with a stronger coding-agent setup for algorithms and scientific code.

19. [**The AI Scientist** - Towards Fully Automated Open-Ended Scientific Discovery](https://arxiv.org/abs/2408.06292) · Lu et al., Sakana AI, 2024  
    End-to-end attempt at automated research in the digital world: ideas, experiments, writeup. Prototype of "autoresearch" before the physical version.

---

## Stage 6 - Physical autoresearch (2026)

Two related NVIDIA GEAR papers (with university collaborators). Do not mash them into one claim.

| | **ASPIRE** | **ENPIRE** |
|--|------------|------------|
| Bet | Code-as-policy + **skill library** that compounds | **Harness** so coding agents can run research on real robots |
| Loop | Write / debug programs from multimodal traces | Reset → improve policy → rollout → evolve (algos + infra) |
| Object of search | Task programs and reusable skills | Policies *and* training recipes on hardware |
| Main leftover work | Frozen primitive API; skill-library hygiene | Building reset/verify/safety so the loop can run |

20. [**ASPIRE** - Agentic /Skills Discovery for Robotics](https://arxiv.org/abs/2607.00272) · Lu, Wu, Kou et al. (incl. Goldberg, Zhu, Fan, Wang), NVIDIA GEAR + Michigan / UIUC / Berkeley / CMU, 2026 · [project](https://research.nvidia.com/labs/gear/aspire/) · **read deeply**  
    Full name: **Agentic Skill Programming through Iterative Robot Exploration**. Three pieces: closed-loop robot execution engine (rich multimodal traces), expanding skill library (validated fixes become reusable text skills), evolutionary search over programs and task sequences. Writes and repairs code-as-policy; experience compounds instead of vanishing after one task. Still bounded by a predefined primitive API - their limitations section is worth reading carefully.

21. [**ENPIRE** - Agentic Robot Policy Self-Improvement in the Real World](https://arxiv.org/abs/2606.19980) · Xiao, Xie et al. (incl. Goldberg, Fan, Zhu, Shi), NVIDIA GEAR + CMU + Berkeley, 2026 · [project](https://research.nvidia.com/labs/gear/enpire/) · **read deeply**  
    Names the game *physical autoresearch*. Four modules: **EN**vironment (auto reset + verify), **PI**olicy Improvement (agents edit training / policy code), **R**ollout (single robot or fleet), **E**volution (compare branches, keep what works on hardware). Coding agents can try heuristics, BC, offline/online RL, infra changes - not only one-shot CaP patches. Fleet experiments come with utilization-style metrics (MRU, MTU), not magic free scaling. If ASPIRE is "skills that stick," ENPIRE is "make the lab loop agent-operable."

---

## How I'd actually read this

1. Stage 0 fast (ReAct + Reflexion) so the robot papers feel familiar.
2. Deep: **Code as Policies** → **Eureka** → **Voyager** → **ASPIRE** → **ENPIRE**.
3. Skim Stage 4 so you can answer "what about VLAs?" without hand-waving.
4. When stuck, open the related-work section of ENPIRE or ASPIRE - those bibliographies are maps.
5. Keep asking: *what is still human-built here?* The honest answer is usually the API, the harness, the success metric, and the safety layer.

---

## Source notes

- Links point at arXiv abstracts, Nature, or project pages where those are more canonical.
- ASPIRE arXiv title uses "Agentic /Skills Discovery"; the expansion used in the paper is *Agentic Skill Programming through Iterative Robot Exploration*.
- ENPIRE arXiv: 2026-06-18. ASPIRE arXiv: 2026-06-30. Thematic order above is skills-then-harness; calendar order is nearly simultaneous.
- FunSearch: Nature article is the main public link (no single canonical arXiv abstract in the same way as the others).
- Numbers and "99%" claims: always check the metric definition on the project page before quoting in a talk.

---

*List started while tracing agentic robotics for talks and product work at Dimensional. Format inspired by [jrin771/Frontier_Robotics_Reading_List](https://github.com/jrin771/Frontier_Robotics_Reading_List).*
