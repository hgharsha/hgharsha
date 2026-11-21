# Z8 G4 project: session summary (2026-11-21)

Read this first in a new session. Related files in this repo: `z-workstation-burn-in-checklist.md`, `ai-architect-roadmap.md`.

## How the owner wants to work
- Truth wins (satyameva jayate). Trust but verify: tell them when unsure and where to check.
- Agile: short sprints, one next action at a time. Owner states what they want, Claude handles the how.
- Ask questions, suggest the best forward path, save notes to a file.
- Owner works in IT, wants to become an AI architect, maybe an entrepreneur (private, low-hardware AI for companies). Learning-driven, budget is zero for now.

## The machine
- HP Z8 G4, refurbished (about 2017), bought on eBay.
- 2x Xeon Platinum 8160 (48 cores, 96 threads), 128 GB RAM (DDR4 ECC RDIMM), 1 TB SSD, Quadro P4000 (8 GB, Pascal), Windows 11 preinstalled.
- Windows is fully backed up by the owner (restore not yet proven).
- eBay listing says no returns. Only the eBay Money Back Guarantee applies (covers "not as described" and faults, not change of mind). Claim deadline is NOT confirmed: check the order page. Screenshot the listing and keep the delivery date.

## Test results so far (HP PC Hardware Diagnostics UEFI, version 2.3.8.0, F2 at boot)
- Memory Test: only a Quick Test exists in this version (about 59 minutes at 128 GB). PASSED.
- Processor test: PASSED. Storage test: PASSED. System Board test: PASSED.
- The owner also ran a 15-minute CPU stress test from the BIOS tool. Windows stress tests not yet done.
- Not yet done: deep memory test (MemTest86, overnight), Windows stress tests, GPU stress, Ubuntu live boot check.

## Next steps (in order)
1. Windows checks: Task Manager shows 2 sockets, 48 cores, 96 logical processors, about 128 GB. No Device Manager warnings. Event Viewer, System log, source WHEA-Logger: any entries are hardware errors, photograph them.
2. CrystalDiskInfo: SSD health, power-on hours, data written.
3. HWiNFO64 plus Prime95 or OCCT: 1-2 hours CPU stress. Confirm all 96 threads load (Windows splits more than 64 threads into two groups; some tools only load one). Watch temperatures (concern above about 90 C), crashes, reboots.
4. Memory stress in Windows (Prime95 Blend or OCCT memory), then GPU stress (FurMark or OCCT) for 15-30 minutes.
5. Boot Ubuntu stick: F9, choose "Try or Install Ubuntu", then "Try Ubuntu" (do not install). If the screen is black or garbled, use "Ubuntu (safe graphics)". In a terminal run `free -h`, `lscpu | head -20`, `lsblk`, `sudo dmidecode -t memory`. Send the output to Claude.
6. MemTest86 (PassMark, free) from USB overnight for the deep memory check. Photograph the result.
7. Photograph every result screen. On any failure, note the failure ID and 24-character code and open the eBay claim promptly.

## Installing Ubuntu (later, after validation)
- Verify the Windows backup restores, and have a recovery USB.
- Check BIOS storage mode (AHCI/NVMe instead of RAID/VMD if the drive is missing) and Secure Boot.
- Owner plans to wipe and reinstall once satisfied. Safer alternative: dual boot (shrink C: in Windows, disable Fast Startup with `powercfg /h off`, suspend BitLocker if on, install alongside Windows Boot Manager, never "Erase disk"). Keeping Windows until the eBay window closes makes a claim easier to defend.
- After install: `sudo apt update && sudo apt upgrade`, `sudo ubuntu-drivers install`, reboot, check `nvidia-smi`, `lscpu`, `free -h`, `sudo smartctl -a /dev/nvme0n1`.

## Upgrade plans (no budget yet)
- RAM: add 2x 64 GB used RDIMM later, maybe up to 1.3-1.4 TB over time. Match RDIMM vs LRDIMM, speed and rank. Populate evenly across both CPUs and the 6 channels per CPU. Test each new batch. Check HP's memory population guide. Check how the current 128 GB is populated with `dmidecode`.
- GPU: used 24 GB card (RTX 3090) next year. Verify Z8 G4 PSU rating, PCIe power cables, slot spacing and cooling before buying. Multi-GPU (2-3) needs a power check.

## AI learning plan
- Now (CPU + RAM + P4000, no training): llama.cpp (build with CUDA 12.x for Pascal), run a small MoE model, then a roughly 100B MoE such as gpt-oss-120b (about 60-65 GB quantized). Use `numactl --interleave=all`. Keep experts in RAM and attention on the GPU (`--n-cpu-moe` or `-ot`).
- Project A: RAG with citations over public documents. Project B: document extraction to JSON. Build a 30-50 item evaluation set for both.
- RAG is for facts and private documents. Fine-tuning is for behavior, format and narrow tasks, and is unreliable for teaching facts. Ladder: prompting, then RAG, then fine-tuning.
- Later with a 24 GB GPU: QLoRA fine-tuning, distillation, evaluation tooling.
- Industry-neutral use cases: private document Q&A, extraction, IT helpdesk assistant, meeting summaries, policy checker, ticket triage. Public pharma data (DailyMed, openFDA, ClinicalTrials.gov, PubMed, ChEMBL) is good practice data.
- Business reality: models are commodities, value is in data pipelines, evaluation, deployment and security. Low-hardware training tools already exist (LoRA/QLoRA, Unsloth, Axolotl, llama.cpp), so use them. Validate with real pilot users first. Never practice on confidential employer or client data.

## Things Claude was unsure about (verify yourself)
- Claude first said the HP Memory Test menu would offer Quick and Extensive. It did not (corrected).
- Z8 G4 Linux support, PSU and cable limits for a 3090.
- Whether CUDA 13 and current PyTorch builds still support Pascal (believed dropped).
- Model sizes and tokens-per-second estimates (measure on the machine).
- eBay claim deadline and terms.
- Temperature thresholds for the Xeon 8160 (check Intel's spec).

## Open questions
- Which area of IT the owner wants as the first niche, goal for the next 2-3 months, weekly time available, and who the first customer or employer might be.
- Output of the Ubuntu live session commands.
