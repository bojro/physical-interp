<img src="logo.svg" alt="Physical Interp Labs logo" width="72">

# Physical Interp Labs

**Bringing mechanistic interpretability to physical AI.**

> **Latest work: [Inherited Heads](https://arxiv.org/abs/2609.14174)** (arXiv:2609.14174, September 2026, sole author)
>
> Fewer than a tenth of an audio language model's attention heads decide which of six speakers it describes, and those heads are inherited from the text-only model it was built on. Adding a fixed bias to about 100 heads, with no training, redirects the model to any chosen speaker on 90.7% to 99.0% of trials. Rank the *text* backbone on a written version of the task, carry its top heads over unchanged, and they steer the audio model on 80.8% to 95.0% of trials, with nothing about audio entering the selection. Tested on three models (Qwen2-Audio-7B, Ultravox-8B, SALMONN-13B), run in 4-bit on consumer GPUs.

Physical Interp Labs studies the internals of neural networks that act in the physical world: robot policies, vision-language-action (VLA) models, and world models used for robotics and drones. The goal is to make these models legible: to find the features and circuits that drive an action, and to use them to predict, steer, and verify behavior before it reaches hardware.

## Why this matters

Learned policies are moving onto real robots and drones fast. VLA models, diffusion policies, and reinforcement-learning controllers already fly, grasp, and drive. Almost all of them are evaluated the same way: run the policy, count successes. That tells you *whether* it works on the cases you tried. It tells you nothing about *why*, and nothing about the cases you did not try.

This project comes from direct experience with that gap. Training a PPO flight policy across 4,096 parallel simulations in NVIDIA Isaac Lab for the Anduril AI Grand Prix, then putting it on a real quadrotor, surfaced faults that no amount of simulation could show: a reversed pitch axis, stick commands scaled anywhere from 0.62x to 2.4x, a control link running at a different rate than the policy assumed. Each was found by hardware-in-the-loop testing, after the fact. Every one of them lived inside the policy's inputs and outputs, and in principle could have been read off the network before the first flight.

Mechanistic interpretability is the toolkit for doing that reading. In language models it has located the circuits behind specific behaviors, found interpretable features with sparse autoencoders, and steered models by editing a handful of components. Inherited Heads showed that the same approach works on a multimodal model and produces a precise, causal result: a small, identifiable set of heads controls a behavior, and that set is traceable to the backbone the model was built from.

Physical AI models are built the same way. Most VLAs start from a pretrained vision-language backbone and add an action head. World models for robotics are built on transformers and diffusion models whose internals are increasingly well understood. The techniques transfer. What is missing is the work of applying them to action, where the stakes are physical and the behavior is continuous.

Understanding the internals of these models matters for:

- **Safety.** Finding what a policy is actually attending to, and whether it has learned a shortcut that will fail outside the training distribution, before it is flown.
- **Debugging.** Locating a failure inside the network instead of bisecting it through flight tests.
- **Reliability.** Evidence about when a model's behavior can be trusted that is stronger than an aggregate success rate.
- **Steering.** Correcting a behavior by editing a small set of components, with no retraining, as Inherited Heads did for speaker selection.

## Research directions

This is planned and ongoing exploratory work, not results.

- **Inherited circuits in VLAs.** VLA models are built on vision-language backbones. Inherited Heads found that an audio model's task-critical heads came from its text backbone. The direct follow-up: do the heads and features that drive a VLA's actions come from its backbone, and can they be found by ranking the backbone alone?
- **Feature discovery in action models.** Sparse dictionary methods (sparse autoencoders and successors) on the activations of open VLA and robot policy models, looking for features tied to perception, planning, and motor output.
- **Circuit analysis of control behavior.** Tracing how a specific input (an obstacle, a target, a gate, a command) propagates through the network to the action taken, and whether editing a small component set can redirect it, as it did for speaker selection.
- **Representations in world models.** Whether world models used for robotics and drones encode physical quantities such as position, velocity, and contact in a readable, steerable way.
- **Tooling.** Adapting interpretability tooling built for language models to the multimodal, continuous-action setting, including the sweep-and-verify harness built for Inherited Heads.

## Prior interpretability work

- **[Inherited Heads: Audio language models track speakers with their text backbone's attention, and an attention-mass ranking retrieves a different set](https://arxiv.org/abs/2609.14174).** Bojro Das, arXiv:2609.14174, September 2026. Sole-authored preprint, 20 pages. Written at Cornell's Math + AI Lab. The harness behind it swept 12,000 configurations over six 7B to 13B models in 4-bit on consumer GPUs, with a build check that rejects any figure not traceable to a run.
- **Independent evaluation of PLOT-DAS**, a published method for locating where a language model represents a causal variable, confirming its reported 10x to 25x compute reduction on the public MIB benchmark with a 126-test suite on one 8 GB GPU.

## Founder

**Bojro Das** studies Mathematics and Computer Science at Cornell University (class of 2028) and has been building robots since well before that.

- **VEX Robotics.** Led a team to the 1st seed at the VEX Robotics World Championship.
- **Anduril AI Grand Prix, autonomous drone racing (2026).** One of 15 teams selected from over 3,000 for the in-person qualifier. Trained the PPO flight policy in Isaac Lab, found and fixed the sim-to-real faults through hardware-in-the-loop testing, and built the onboard gate detector running at 36 fps on the drone's Jetson Orin NX.
- **Cornell University Autonomous Drone (CUAD).** Software engineer on the autonomy subteam. Built a real-time stereo-depth obstacle-localization pipeline publishing to ROS 2 at 15 Hz for the IARC competition, and a gesture-to-flight-command classifier deployed as ROS 2 nodes.
- **Drone telemetry gateway.** A Go service ingesting telemetry from 1,000 simulated drones over MQTT, sustaining 5,000 writes per second to PostgreSQL with zero accepted-message loss through a measured database outage.
- **Interpretability.** Sole author of Inherited Heads, above.

Robotics and interpretability are the two things this project's founder has spent the most time on. Physical Interp Labs is where they meet.

## Current status

Early-stage research. There is no product, no users, and no external funding. Experiments currently run on a laptop and rented cloud GPUs, with plans to move to AWS as the work grows. Code, notes, and experiment writeups will be added to this repository as the work progresses.

## License

MIT. See [LICENSE](LICENSE).
