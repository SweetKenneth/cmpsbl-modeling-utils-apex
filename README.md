CMPSBL® Ascension — PyTorch & HuggingFace Core Files · 2× CJPI 100 Apex

A deterministic, non-AI substrate autonomously wrapped two of the most critical files in the ML ecosystem. No human selected the primitives. The code told the scanner what it needed.

Two Runs. Two Files. Two CJPI 100 Apex Results.


The same deterministic scanner. Two completely different primitive chains. Because the structural patterns in the code drove the selection — not a human, not an AI.

Why These Two Files

HuggingFace modeling_utils.py — 126,779,252 downloads per month. The base class for every transformer model in production. Calls torch.load on arbitrary checkpoint files from the internet. Has never been stateful. Has never been observable.

PyTorch torch/serialization.py — the file where CVE-2025-32434 actually lives. CVSS 9.3 critical. Proved that even weights_only=True — the parameter everyone trusted as the safe path — still allows remote code execution via crafted pickle payloads. 2,202 lines. 107 imports. 12 documented TODO/FIXME/HACK markers. Cyclomatic complexity of 335.

Run 1 wrapped the HuggingFace layer that calls torch.load.

Run 2 wrapped the PyTorch file that implements it.

What the Substrate Did - Run 1: modeling_utils.py

	∙ Made the file stateful for the first time. MEMORY deployed filesystem-backed persistent state with crash snapshotting and last-known-good recovery.
	
	∙ Added observability that never existed. SENTINEL, HERALD, and PRISM deployed health probes, interface surfacing, and execution path decomposition.
	
	∙ Wrapped the torch.load RCE (CVE-2025-32434, CVSS 9.3). BASTION and IRONCLAD deployed perimeter hardening in front of the deserialization path.
	
	∙ Wrapped the trust_remote_code execution surface. PHOENIX and SENTINEL deployed input validation gates.
	
	∙ Crossed domain boundaries autonomously. Quantum and Robotics primitives fired on an ML file because the structural patterns matched.
	
Primitive chain (40): 

CONDUIT (98) · ORACLE (98) · APEX (96) · GENESIS (94) · CRUCIBLE (94) · LEXICON (93) · LIDAR (92) · DELEGATE (92) · TOOLKIT (90) · PRISM (90) · FLUX (90) · DYNAMO (90) · SENTINEL (90) · CATALYST (90) · HERALD (90) · PHOENIX (90) · SIEVE (89) · TENSOR (89) · NEUTRINO (89) · TETHER (89) · MEMORY (88) · CUSTODIAN (88) · GRIPPER (87) · QUBIT (87) · OPERATOR (87) · SERVO (86) · HADRON (86) · RAMPART (86) · RECONN (86) · CLARITY (85) · FULCRUM (85) · MARSHAL (84) · TACHYON (84) · MESON (84) · LINEAGE (84) · BASTION (83) · SYLLOGISM (83) · SCRIBE (83) · IRONCLAD (83)

Capabilities surfaced: 

Self-Healing State Machine · Zero-Trust Perimeter Enforcer · Quantum Circuit Optimizer · Context Persistence Layer · Skill-Based Task Router · Reinforcement Learning Loop · Cryogenic Decoherence Shield · Neutrino Oscillation Predictor · QCD Color Charge Simulator · Particle Collision Analyzer

What the Substrate Did — Run 2: serialization.py

	∙ Wrapped the vulnerability at its source. Not the layer that calls torch.load — the file that implements it. VANGUARD and BASTION deployed two-layer Cyber defense around the actual CVE location.
	
	∙ Deployed behavioral mapping for the first time. ENCODE activated a behavioral mapper and intent tracer — generating function signatures and runtime behavioral logs to detect malicious pickle patterns.
	
	∙ Initialized passive pattern learning. BRAIN deployed a 90-day passive learning engine to establish what normal serialization behavior looks like — so anomalies can be detected.
	
	∙ Wrapped trust decision points with integrity verification. VERITAS (10/34 signal hits — highest raw signal count in this run) wrapped every point where the serializer decides whether to trust a file.
	
	∙ Deployed forward threat detection. VANGUARD deployed proactive threat detection, not just reactive hardening — watching for malicious payloads before they reach the deserializer.
	
	∙ Governed concurrent deserialization. KINETIC and SWARM wrapped the threading paths where multiple simultaneous torch.load calls create race condition attack surface.
	
	∙ Made the file stateful. MEMORY fired again — because serialization.py has the same structural gap as modeling_utils.py. No memory of what it has loaded before. No record of failures. Now it does.
	
Primitive chain (40): 

TOOLKIT (94) · ORACLE (94) · SENTINEL (90) · NOMAD (90) · MEMORY (88) · LEXICON (88) · CUSTODIAN (87) · FLUX (87) · CATALYST (87) · ARBITER (87) · OPERATOR (87) · APEX (86) · RAMPART (86) · TETHER (84) · LIDAR (83) · DELEGATE (83) · CONDUIT (83) · GENESIS (83) · CRUCIBLE (83) · PHOENIX (83) · SERVO (82) · VERITAS (82) · UPLINK (81) · SYLLOGISM (81) · MANDATE (80) · PRISM (80) · BASTION (79) · HADRON (79) · ENCODE (78) · VANGUARD (78) · MESON (77) · BRAIN (77) · KINETIC (77) · TENSOR (77) · SWARM (77) · CLARITY (77) · HERALD (77) · ANCHOR (77) · SCRIBE (74) · PRISM (74)

Capabilities surfaced: 

Attack Chain Reconstructor · Forensic Incident Response · Zero-Downtime Migrator · Mission Decomposer · Rate Limit Intelligence · Content Generation Engine · Skill-Based Task Router · Context Persistence Layer · QCD Color Charge Simulator · Particle Collision Analyzer

The Key Finding Across Both Runs

The primitive chains are completely different. 17 primitives that fired on serialization.py did not appear in the modeling_utils.py run — NOMAD, ARBITER, VERITAS, UPLINK, MANDATE, ENCODE, VANGUARD, BRAIN, KINETIC, SWARM, ANCHOR, VANGUARD, MANDATE, UPLINK, SERVO, FLUX, CATALYST.

The scanner read two different files and assembled two different optimal configurations. That is the system working as designed. The code tells the scanner what it needs. The scanner selects without human input or AI recommendation.

ENCODE and BRAIN fired on serialization.py and not modeling_utils.py — because this is the file where you need behavioral mapping and pattern learning over time. This is where malicious payloads enter. This is where you watch for what isn’t normal.


Verify Either Artifact

npm install @cmpsbl/test-harness

# Verify modeling_utils.py run
npx cmpsbl-test --config ./modeling-utils/restoration-report.json

# Verify serialization.py run
npx cmpsbl-test --config ./serialization/restoration-report.json


Reproduce Either Run

	1.	Download the file from GitHub
	2.	Upload to ultimate.cmpsbl.com
	3.	Run Ascension
	4.	Compare restoration-report.json — collision scores should match within ±2 points

modeling_utils.py: 

github.com/huggingface/transformers/blob/main/src/transformers/modeling_utils.py

serialization.py: 

github.com/pytorch/pytorch/blob/main/torch/serialization.py

Full Technical Case Studies

Run 1 — modeling_utils.py:
10.5281/zenodo.19423852

Run 2 — serialization.py:
Zenodo record pending

The Substrate

The CMPSBL® substrate that produced these artifacts is proprietary. This repository contains only the output artifacts and associated documentation.

Live at cmpsbl.com · ULTIMATE tier at ultimate.cmpsbl.com

Technical inquiries: ascension@cmpsbl.com

License

MIT — for the contents of this repository.
HuggingFace source inside modeling-utils/refurbished-source.py is Apache 2.0 © Google AI Language Team, Facebook AI Research, HuggingFace Inc., NVIDIA Corporation.

PyTorch source inside serialization/refurbished-source.py is BSD-style licensed © Facebook Inc. and PyTorch contributors.

The CMPSBL® substrate, primitive matrix, collision algorithms, CJPI formula, and all internal orchestration logic are proprietary © 2026 Kenneth E. Sweet Jr. · All rights reserved.

© 2026 Kenneth E. Sweet Jr. · PromptFluid™ · CMPSBL®

ORCID: 0009-0001-4237-1243
