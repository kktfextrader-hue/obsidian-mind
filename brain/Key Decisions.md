---
description: "Architectural and workflow decisions worth recalling across sessions — each links to its source work note"
tags:
  - brain
date: 2026-10-16
---

# Key Decisions

Architectural or workflow decisions worth recalling. Link to the full [[Decision Record]] when one exists.

- **2026-10-16 — mdกลาง/ai-shared consolidation (Phase 1 docs only, qbank move deferred until after exams):**
  - a2a ปัจจุบัน = Muxi chat (`127.0.0.1:8001/v1/chat`) + Switch/ops-hub เท่านั้น — ยืนยันซ้ำโดยผู้ใช้ 2026-10-16, แก้ `F:\MD\systems\crux-agent\README.md` Runtime section ที่ยังอ้าง `E:\a2a` port 9903 (deleted infra) ให้ตรง
  - **กฎใหม่ CONFLICT-ASK-USER-001** (`F:\MD\README.md` rule 7): เจอข้อมูลขัดแย้งกันระหว่างเอกสาร ห้ามเลือกเองว่าอันไหนถูกแล้วแก้เงียบๆ ต้องถามผู้ใช้ก่อน ยกเว้นมี ground-truth ชัดเจน (grep นับจริง, คำสั่ง owner ที่บันทึกไว้แล้ว) — เหตุ: agent เคยอ้าง `kb.md:145` ผิด (record ที่ไม่มีจริง)
  - **"backup2p" = ชื่อซ้ำของ `backup2gdrive` ที่มีอยู่แล้ว** (`D:\ai-shared\tools\backup2gdrive.py`, Task Scheduler ประจำ 03:00, 2 location: H:+Google Drive) — ตัดสินใจไม่สร้างคำสั่งใหม่ ใช้ `backup2gdrive` ต่อไป กันมี 2 ชื่อของระบบเดียว รายละเอียด `D:\ai-shared\rescue.md`
  - **เลข skill ที่ขัดกัน (65/125/165/170/172)** = สองระบบนับคนละชุดข้อมูล ไม่ใช่ error เดียวซ้อนกัน — runtime set จริง (`D:\ai-shared\skills\_records.json`) = 150 record, ไม่ตรงกับเลขฝั่ง catalog เลย ไม่มี skill ชื่อซ้ำกันภายใน dest dir เดียวกัน (verify แล้ว) รายละเอียดเต็ม `F:\MD\capability-catalog\SKILL_AGENT_MAPPING.md`
  - qbank 4-ที่ (`D:\ai-shared\qbank`, `F:\MD\projects\qbank`, `F:\MD\systems\qbank` locked, `H:\ai-shared-extend\qbank`) ยังไม่รวม — ผู้ใช้สั่งชัด "จะทำหลังข้อสอบเสร็จ" แผนเต็มอยู่ `C:\Users\acer\.claude\plans\glistening-hugging-frost.md`
  - PENDING subagent skills (video-production/avatar-studio/graphic-design) ยืนยันแล้วว่าไม่มีจริงในระบบ (grep ซ้ำหลายจุด) — ถือว่าไม่มี ไม่ต้องตามหาต่อ ตามที่ผู้ใช้สั่ง
