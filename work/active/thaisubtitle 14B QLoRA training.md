---
title: thaisubtitle 14B QLoRA training
date: 2026-10-14
tags:
  - project
  - active
status: in-progress
description: Train Qwen2.5-14B-Instruct via QLoRA on free Colab A100 to beat the 7B distill's SAP/FLORES scores; recurring disconnect/rebuild cycle, step 2153/2711 at handoff, re-upload pending.
quarter: 2026-Q4
---

# thaisubtitle 14B QLoRA training

Closing the quality gap for the `thaisubtitle` (`D:\ai-shared\projects\thaisubtitle`) EN→TH subtitle translation model. The 7B QLoRA distill already reached SAP 14.28 / FLORES 8.23 (94% of Typhoon teacher's 15.19/8.99), short of the project target SAP ≥14.43 / FLORES ≥8.54 by 0.15/0.31.

## Approach

Train Qwen2.5-14B-Instruct via QLoRA (4-bit bitsandbytes) on free Google Colab Pro L4 GPU, instead of the originally planned Modal A100 run (~$7) — per explicit cost-safety instruction to use free compute first.

- Dataset: `dataset/distill/train_typhoon.jsonl` (88,532 rows, Typhoon teacher)
- Recipe mirrors `modal_train.py`: LoRA r=64/alpha=128/dropout=0.05 on q/k/v/o/gate/up/down proj
- Scope reduced to **1 epoch** (~2711 steps, ~17h estimated) after a smoke-test estimation bug projected 92min instead of the real ~34h for 2 epochs
- Checkpoints save every 200 steps to Google Drive (`thaisubtitle_ckpt/qwen25-14b-qlora-v1`) for resume across Colab sessions

## Status (2026-10-15)

- Runtime kept disconnecting/reallocating repeatedly throughout — at least 4 full rebuild cycles so far (mount → re-upload script+dataset → pip install → sed-patch → resume)
- Each Colab runtime reset wipes `/content` (script + dataset + the `_patch.py`/sed edits), requiring the full rebuild sequence again every time — this is now a well-worn, reliable drill, not a blocker
- Resume hits a PyTorch 2.6 `weights_only=True` default-flip bug in `transformers/trainer.py`'s `_load_rng_state`. Fixed every time by `sed`-patching `trainer.py` line ~3033 to force `weights_only=False` on that one `torch.load` call (monkeypatching `torch.load` from the script doesn't stick)
- `bitsandbytes` must be installed **unpinned** (`pip install -q -U bitsandbytes`, not `==0.44.1`) on a fresh A100 runtime, or it crashes with `No module named 'triton.ops'` — the notebook's cell 3 still has the old pinned install; cell 12 (`!pip install -q -U bitsandbytes`) is the fix and must run AFTER cell 3 every rebuild
- Progress despite the churn: resumed cleanly from checkpoint-400 → reached **step 2153/2711 (79%), loss 0.4866, eval_loss 0.477 at step 2000** before the latest disconnect (2026-10-15 ~04:11). A100 Colab Pro compute units: 106.51 remaining (~15.7h headroom at current ~6.77/h burn rate), monthly renewal — not a constraint
- **IN PROGRESS at handoff**: notebook auto-ran "Run all" after reconnect, stopped at an old stale test cell (`colab_train_14b.py --max-steps 20`, expected error, file wiped). `/content` currently only has `drive/`, `sample_data/`, `_patch.py`, `_tmp2.py` — **`colab_train_14b.py` and `train_typhoon.jsonl` need re-upload** via the Colab Files pane before training can resume. File Explorer was opened to `D:\ai-shared\projects\thaisubtitle` for this; upload not yet confirmed done.
- H:\ai-backup off-site backup to Google Drive (`gdrive:ai-backup-offsite`, via rclone) completed separately this session — 30.26GiB, unrelated to training but shares the same GDrive account/quota (1.17TB+ free, no conflict)

## Open Questions

- Is Colab's session volatility (disconnect before checkpoint) going to make this impractical vs. just paying for the Modal A100 run? — leaning toward "tolerable": each rebuild cycle now takes ~10-15min and the checkpoint/resume logic is proven reliable
- Worth fixing the smoke-test step-count estimation bug in `colab_train_14b.py` before relying on it again?
- **Should fold into the setup cells, so the recurring pain stops being manual**: (1) the trainer.py sed-patch, (2) unpinned bitsandbytes install — both currently require remembering to re-apply by hand every single rebuild, and the pinned-bitsandbytes cell (cell 3) is a known trap that will crash training if cell 12's fix is skipped

## Research Methodology (Andrew Ng 5-step, adapted)

Facebook post (Thongchai Thampueak) describes Generate→Backtest→Validate→Analyze→Iterate for trading-strategy research — same shape as [[fable-method]] skill. Mapped onto this project's own loop:

- **Generate**: LoRA config variants (r/alpha/dropout, target modules)
- **Backtest**: SAP/FLORES eval score per checkpoint
- **Validate**: held-out set check (not just the eval set used during training)
- **Analyze**: compare against target SAP ≥14.43 / FLORES ≥8.54 — current 14B run must clear the 7B distill's 14.28/8.23
- **Iterate**: adjust hyperparameters for next round

Rigor reminder (walk-forward / Monte Carlo / parameter-stability style): don't call it a win off one good eval number. Check stability across multiple checkpoints or eval subsets before declaring the quality gap closed — single-point SAP/FLORES at step 2711 isn't enough on its own.

## Related

- [[North Star]]
- [[fable-method]]
