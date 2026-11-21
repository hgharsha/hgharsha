# AI architect learning roadmap (Z8 G4, 128 GB RAM, P4000 now, 3090 later)

Goal: learn to be an AI architect, possibly a consultant or entrepreneur delivering private, low-hardware AI. Not tied to one industry.

## Now (no training, CPU + RAM + P4000)
1. Install Ubuntu LTS and NVIDIA driver, build llama.cpp, run a small MoE model, then a ~100B MoE (gpt-oss-120b class).
2. Project A: private document Q&A (RAG) with citations. Use public documents (for example DailyMed labels).
3. Project B: document extraction to JSON (invoices, forms, trial abstracts).
4. For both: build an evaluation set (30-50 questions or documents with known answers) and track accuracy.
5. Optional: local speech-to-text plus summarization for meetings.

## Later (after a 24 GB GPU such as a 3090)
- QLoRA fine-tune a small model for one narrow task.
- Distillation: label data with a big model, train a small model that runs on cheap hardware.
- Evaluation harness, guardrails, monitoring.

## Reality checks
- Models are becoming commodities. The value is in data pipelines, evaluation, deployment, security and maintenance.
- Low-hardware training tools already exist (LoRA/QLoRA, Unsloth, Axolotl, llama.cpp). Use them, don't compete with them.
- Validate with 1-2 real pilot users before building a product.
- Never use confidential employer or client data for practice.

## Open questions
- Which part of IT does the owner know best? That decides the first niche.
- RAM population (`sudo dmidecode -t memory`) to plan the 64 GB upgrade.
