# Physical Interp Labs

**Bringing mechanistic interpretability to physical AI.**

Physical Interp Labs is an early-stage research project studying the internals of neural networks that act in the physical world: robot policies, vision-language-action (VLA) models, and world models used for robotics and drones.

## Motivation

Mechanistic interpretability aims to understand what a neural network computes internally: the features it represents, the circuits that connect them, and how those give rise to its behavior. Most of this work to date has focused on language models.

Models that control physical systems make decisions with real-world consequences. When a drone or a robot arm does something unexpected, it is not enough to observe that it happened; we want to know why. Understanding the internal representations of these models matters for:

- **Safety.** Identifying what a policy is actually attending to, and whether it has learned shortcuts that could fail outside its training distribution.
- **Debugging.** Locating the source of a failure inside the model rather than treating it as a black box.
- **Reliability.** Building evidence about when a model's behavior can be trusted, beyond aggregate benchmark scores.

## Research directions

This is planned and ongoing exploratory work. None of it should be read as results.

- **Feature discovery in action models.** Applying sparse dictionary methods (such as sparse autoencoders) to the activations of open VLA and robot policy models to find interpretable features tied to perception, planning, and motor output.
- **Circuit analysis of control behavior.** Tracing how specific inputs (an obstacle, a target object, a command) propagate through the network to influence the action taken.
- **Representations in world models.** Examining whether world models used for robotics and drones encode physical quantities such as position, velocity, or contact in a readable way.
- **Tooling.** Adapting interpretability tooling built for language models to the multimodal, continuous-action setting of physical AI.

## Current status

Early-stage research. There is no product, no users, and no external funding. Experiments are currently run on a laptop and rented cloud GPUs, with plans to move to AWS as the work grows.

Code, notes, and experiment writeups will be added to this repository as the work progresses.

## Founder

**Bojro Das** is an undergraduate studying Mathematics and Computer Science at Cornell University (class of 2028). Previously worked on software engineering for CU Auto Drone, Cornell's autonomous drone project team.

## License

MIT. See [LICENSE](LICENSE).
