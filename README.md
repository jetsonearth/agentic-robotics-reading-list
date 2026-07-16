# Agentic robotics reading list

Paper trail from **language-conditioned robot control** to **physical autoresearch** - what I call *agentic robotics*.

Agents mostly still live on screens: they write code, call tools, run workflows. A robot that can plan, act, fail, and revise is that same loop with a body. I traced this backward from NVIDIA's ENPIRE (physical autoresearch) through Eureka to Code as Policies. This list is that trail, cleaned up for people who already build software agents and want the physical side without a robotics PhD.

**Question for every paper:** *What did this hand off from humans to AI?*

**Deep-read:** Code as Policies, Eureka, Voyager, ASPIRE, ENPIRE.  
**Everything else:** abstract + method figure + one results table is enough.

---

## How this list is organized (not "stages of history")

The first version of this list used Stage 1 / 2 / 3 like a single ladder. That was misleading.

- The **agentic / code** line *does* have a natural reading order (later work reuses earlier ideas).
- **VLAs** and **world models** are not "the next stage after skills." They are **parallel bets** the field is making at the same time - different substrates, often composed with agents rather than replaced by them.
- Years overlap. Eureka and FunSearch landed in the same season. Voyager is older than both. Treat the spine as a story about *what got automated*, not a timeline exam.

So the structure is:

1. **Main spine** - the agentic path (digital loops → code policies → rewards → skills → digital autoresearch → physical autoresearch)
2. **Parallel bets** - VLAs, and world models *as robot learning people mean them*
3. **What is still not agentic** - so you do not oversell this in a talk

---

## What is still not agentic (read this before the hype papers)

1. **Frozen interfaces.** ASPIRE-style systems mostly rewrite task code *inside* a fixed perception / planning / control API. They do not reinvent the whole stack.
2. **Humans still build the harness.** ENPIRE needs auto-reset, auto-verify, logging, and safety before coding agents can grind unsupervised. That harness *is* a lot of the product.
3. **Search under a designed interface.** Self-improvement today is mostly search in program space or reward space: propose, run, keep winners. Not unbounded self-invention.
4. **Metrics lie if you skim.** e.g. ENPIRE's high success numbers use a specific pass@k definition (in-context retries in a long loop). Always check the project page before quoting in a workshop.
5. **Tokens are cheap; robot hours are not.** Same agent loop as software, different cost of a bad action.

---

# Main spine - the agentic path

## Digital agent loops (the pattern before the body)

Physical autoresearch is the embodied version of loops software people already know: reason, use tools, observe, revise.

1. [**ReAct** - Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) · Yao et al., 2022  
   Interleave reasoning with tool/environment actions. The basic think → act → look → think skeleton.

2. [**Reflexion** - Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) · Shinn et al., 2023  
   After failure, write a short linguistic self-critique into memory and retry - no weight updates. Debug in language, not only in gradients.

**Same family, no paper required for the arc:** coding agents that edit real repos (Claude Code, Codex, SWE-agent-style systems). Propose code → run tests → read logs → patch. ENPIRE is roughly that loop with a robot farm instead of CI.

---

## Language meets robots (planning, grounding, code as policy)

3. [**SayCan** - Do As I Can, Not As I Say: Grounding Language in Robotic Affordances](https://arxiv.org/abs/2204.01691) · Ahn et al., Google, 2022  
   LLM proposes skills; a value/affordance model scores what the robot can actually do. Grounding problem in one slide: language is cheap, physics is not.

4. [**Socratic Models** - Composing Zero-Shot Multimodal Reasoning with Language](https://arxiv.org/abs/2204.00598) · Zeng et al., Google, 2022  
   Several foundation models talking through language. Context for the CaP circle of ideas.

5. [**Code as Policies** - Language Model Programs for Embodied Control](https://arxiv.org/abs/2209.07753) · Liang et al., Google, 2022 · **read deeply**  
   The hinge of this whole list: the *policy itself* is LLM-generated code, not only a plan over fixed skills. If you deep-read one early paper, this is it.

6. [**ProgPrompt** - Generating Situated Robot Task Plans using LLMs](https://arxiv.org/abs/2209.11302) · Singh et al., NVIDIA / USC, 2022  
   Parallel to CaP: programmatic prompts for task plans. Useful next to CaP (plan-as-code vs policy-as-code).

7. [**Inner Monologue** - Embodied Reasoning through Planning with Language Models](https://arxiv.org/abs/2207.05608) · Huang et al., Google, 2022 · [project](https://innermonologue.github.io/)  
   Environment feedback returns to the LLM as language. Early "run, fail, narrate, repair" template.

---

## Code writes denser objects (maps, rewards, sim-to-real)

Once code is the interface, people generate more than "pick up the cup."

8. [**VoxPoser** - Composable 3D Value Maps for Robotic Manipulation with Language Models](https://arxiv.org/abs/2307.05973) · Huang et al., Stanford, 2023  
   Code builds 3D value maps for motion, not only named primitive sequences.

9. [**Language to Rewards** - for Robotic Skill Synthesis](https://arxiv.org/abs/2306.08647) · Yu et al., Google DeepMind, 2023  
   LLM writes reward functions for an MPC stack. Language shapes the objective; a controller optimizes it.

10. [**Eureka** - Human-Level Reward Design via Coding LLMs](https://arxiv.org/abs/2310.12931) · Ma et al., NVIDIA, 2023 · **read deeply**  
    LLM proposes reward *code*; evolutionary search keeps variants that train better policies. "LLM as reward engineer," not a magic optimizer. Big handoff: humans stop hand-writing every reward.

11. [**Text2Reward** - Reward Shaping with Language Models for RL](https://arxiv.org/abs/2309.11489) · Xie et al., 2023  
    Concurrent with Eureka. Optional contrast if you care about design choices.

12. [**DrEureka** - Language Model Guided Sim-To-Real Transfer](https://arxiv.org/abs/2406.01967) · Ma et al., 2024  
    Eureka-family follow-up: LLM helps domain randomization / sim-to-real, not only the reward.

---

## Skills that stick (open-ended agents, libraries, generative training)

13. [**Voyager** - An Open-Ended Embodied Agent with Large Language Models](https://arxiv.org/abs/2305.16291) · Wang et al., NVIDIA, 2023 · **read deeply**  
    Minecraft, not a robot arm - still the cleanest early demo of coding agent + automatic curriculum + skill library. Pattern ancestor of ASPIRE (shared people and ideas; different world). Experience compounds instead of vanishing after one task.

14. [**RoboGen** - Unleashing Infinite Data for Automated Robot Learning via Generative Simulation](https://arxiv.org/abs/2311.01455) · Wang et al., CMU, 2023  
    Agent proposes tasks, scenes, and training supervision in sim. Another way to keep generating work without a human curriculum every time.

---

## Digital autoresearch (methodology, not robots)

Same *idea class* as Eureka-style program search, pointed at math, algorithms, and paper-writing. Not a strict parent of Eureka - Eureka (Oct 2023) and FunSearch (late 2023) are closer to siblings - but useful before you put the loop on hardware.

15. [**FunSearch** - Mathematical discoveries from program search with large language models](https://www.nature.com/articles/s41586-023-06924-6) · Google DeepMind, Nature, 2023 · [blog](https://deepmind.google/blog/funsearch-making-new-discoveries-in-mathematical-sciences-using-large-language-models/)  
    LLM proposes programs; evolutionary search keeps winners. Modern LLM flavor of program search (the idea is older than LLMs).

16. [**AlphaEvolve** - A coding agent for scientific and algorithmic discovery](https://arxiv.org/abs/2506.13131) · Novikov et al., Google DeepMind, 2025 · [announcement](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)  
    Stronger coding-agent setup for algorithms and scientific code.

17. [**The AI Scientist** - Towards Fully Automated Open-Ended Scientific Discovery](https://arxiv.org/abs/2408.06292) · Lu et al., Sakana AI, 2024  
    End-to-end digital research attempt: ideas, experiments, writeup. Autoresearch prototype before the physical version.

---

## Physical autoresearch (2026)

Two related NVIDIA GEAR papers (with university collabs). Same ecosystem, different claims - do not mash them.

| | **ASPIRE** | **ENPIRE** |
|--|------------|------------|
| Bet | Code-as-policy + **skill library** that compounds | **Harness** so coding agents can research on real robots |
| Loop | Write / debug programs from multimodal traces | Reset → improve policy → rollout → evolve (algos + infra) |
| Search object | Task programs and reusable skills | Policies *and* training recipes on hardware |
| Still human-heavy | Frozen primitive API; skill-library hygiene | Reset / verify / safety so the loop can run |

18. [**ASPIRE** - Agentic /Skills Discovery for Robotics](https://arxiv.org/abs/2607.00272) · Lu, Wu, Kou et al. (incl. Goldberg, Zhu, Fan, Wang), NVIDIA GEAR + Michigan / UIUC / Berkeley / CMU, 2026 · [project](https://research.nvidia.com/labs/gear/aspire/) · **read deeply**  
    Expansion: **Agentic Skill Programming through Iterative Robot Exploration**. Closed-loop execution engine (rich traces), skill library (validated fixes become reusable text skills), evolutionary search over programs and task sequences. Experience sticks. Still bounded by a predefined primitive API - read their limitations section.

19. [**ENPIRE** - Agentic Robot Policy Self-Improvement in the Real World](https://arxiv.org/abs/2606.19980) · Xiao, Xie et al. (incl. Goldberg, Fan, Zhu, Shi), NVIDIA GEAR + CMU + Berkeley, 2026 · [project](https://research.nvidia.com/labs/gear/enpire/) · **read deeply**  
    Names *physical autoresearch*. Modules: **EN**vironment (auto reset + verify), **PI**olicy Improvement, **R**ollout (one robot or fleet), **E**volution (keep what works on hardware). Agents can try heuristics, BC, offline/online RL, infra changes - not only one-shot CaP patches. Fleet work reports utilization-style metrics (MRU, MTU), not free scaling magic. ASPIRE: skills that stick. ENPIRE: make the lab loop agent-operable.

---

# Parallel bets - not later stages of the same story

If the workshop only covered the agentic spine, someone will ask "what about π0 / OpenVLA / world models?" These are **other ways to spend the same industry budget**, not steps 4 and 5 after Voyager.

A crude triangle:

| Bet | Core move | Typical substrate |
|-----|-----------|-------------------|
| **Agentic / code** | LLM or coding agent searches programs, rewards, research steps under tools + feedback | Code, APIs, skill libraries, harnesses |
| **VLA** | Train (or finetune) a policy that maps vision + language → actions end-to-end | VLM backbone + robot data |
| **World model (robot learning sense)** | Learn dynamics / predictors so you can plan, imagine, or train in a learned sim | Latent dynamics, action-conditioned predictors - *not* "cool video demos" by themselves |

In practice labs compose these. An agent can sit on top of a VLA API. A world model can sit under RL that Eureka-style reward code trains. The triangle is for orientation, not purity contests.

---

## VLA route

Same recipe family: take a strong multimodal backbone, specialize it for robot actions.

20. [**RT-2** - Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://arxiv.org/abs/2307.15818) · Google DeepMind, 2023  
    Early canonical VLA: web-scale vision-language knowledge into robot actions.

21. Pick one modern VLA if you only have time for one more:
    - [**π0** - A Vision-Language-Action Flow Model for General Robot Control](https://arxiv.org/abs/2410.24164) · Physical Intelligence, 2024 - usually the better single read
    - [**OpenVLA** - An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246) · Kim et al., Stanford / Berkeley, 2024 - if you care about open weights / reproducible stack

You do **not** need every VLA paper for an agentic-robotics workshop. One early (RT-2) + one current is enough to answer the room.

---

## World model route (robot learning sense)

When robot-learning people say "world model," they usually mean something you can **condition on actions** to predict future state / observation and then **plan or train** against - latent dynamics (Dreamer-style), learned sims, world-action models, etc.

That is **not** the same pile as "video generation models that look interactive." e.g. Genie is interesting generative video work; for *this* list it is mostly a distraction. Some later systems *do* finetune a video backbone for control - that recipe is closer to VLA (backbone → action) than to classical world-model RL. Do not confuse the three in a talk.

22. [**DreamerV3** - Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104) · Hafner et al., Google DeepMind, 2023  
    Clear modern reference for *learn a latent world model, act inside it*. Not robot-specific, but this is what people mean by world-model RL more often than a video demo.

23. [**UniSim** - Learning Interactive Real-World Simulators](https://arxiv.org/abs/2310.06114) · Yang et al., Berkeley / Google DeepMind, 2023  
    Action-conditioned interactive sim from real-world data - closer to "use a learned world for robot-relevant interaction" than pure video generation. Optional; read if you want one robotics-adjacent world-model paper beyond Dreamer.

**Skip for this workshop arc:** pure generative interactive video papers (Genie and friends) unless your talk is specifically about video backbones for control - and if it is, say that recipe out loud so it does not get smuggled in as "the world model route."

---

## How I'd actually read this

1. ReAct + Reflexion in 20 minutes so robot loops feel familiar.
2. Deep spine: **CaP → Eureka → Voyager → ASPIRE → ENPIRE**.
3. Skim RT-2 + π0 (or OpenVLA) so you can answer the VLA question.
4. Skim DreamerV3 (and UniSim only if curious) so "world model" means the right thing in the Q&A.
5. When stuck, open related work in ENPIRE / ASPIRE - those bibliographies are maps.
6. Keep asking: *what is still human-built?* Usually the API, the harness, the success metric, and safety.

For a **software-engineer workshop** (non-roboticists): spend 70% of the talk on the main spine + limits, 20% on the triangle of bets, 10% on "how you would start this weekend" (agent + robot API + reset/verify). Do not make people read Genie to understand agentic robotics.

---

## Source notes

- Links are arXiv abstracts, Nature, or project pages where those are more canonical.
- ASPIRE arXiv title: "Agentic /Skills Discovery"; paper expansion: *Agentic Skill Programming through Iterative Robot Exploration*.
- ENPIRE arXiv 2026-06-18; ASPIRE arXiv 2026-06-30. Nearly simultaneous; table above is by claim, not by calendar.
- FunSearch: Nature article is the main public link.
- Quote metrics only after checking the project page definition.

---

*Started while tracing agentic robotics for talks and product work at Dimensional. Format inspired by [jrin771/Frontier_Robotics_Reading_List](https://github.com/jrin771/Frontier_Robotics_Reading_List).*
