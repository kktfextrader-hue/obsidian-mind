---
description: "Recurring patterns and conventions discovered across work — architecture, naming, tooling, and implementation patterns"
tags:
  - brain
date: 2026-10-16
---

# Patterns

Recurring patterns discovered across work.

- **เช็ค mdกลาง (`F:\MD\capability-catalog\`) ก่อนรัน crux-v2 ทุกครั้งที่มีลิงก์ repo/tool ใหม่เข้ามา — อ่าน index file ก่อน ไม่ใช่ grep เดากระจาย:**
  - `CRUX_UNIFIED_MASTER_CATALOG.md` — ทางเข้าหลัก (skill+PL+repo+tool ทั้งหมด)
  - `MASTER_SKILL_INDEX.md` — รายการ skill ทั้งหมด (165+)
  - `ALL_REPOS_MASTER_INDEX.md` + `INSTALLED_TOOLS_INDEX.md` — repo/tool ที่ลงทะเบียน
  - `SKILL_TAXONOMY_ROUTER.md` — หา skill ตามสถานการณ์ถ้าไม่รู้ชื่อ
  - `kkcallmd-skills\kb.md` — fact-note/pilot log ละเอียด (ตัว index ด้านบนอาจชี้มาที่นี่)
  - **ทำไม:** เคยเจอ 3/10 repo จากโพสต์ Instagram ซ้ำของเดิมที่เคยประเมินแล้ว (Ponytail = ปฏิเสธแล้วซ้ำ `/simplify`+`/code-review`, UI/UX Pro Max = ติดตั้งแล้ว 8 skill, Diagram Design = adopt แล้ว) grep มั่วทั่วโฟลเดอร์แพง/ช้ากว่าเปิด index file ที่มีอยู่แล้วตรงจุด
  - **ใช้เมื่อ:** ผู้ใช้วางลิงก์ repo เดี่ยวหรือ list/screenshot หลายตัวมาให้ประเมิน — เปิด index หาทุกชื่อก่อน รายงานว่าตัวไหนรู้จักแล้ว (adopt/reject/pilot/mention-only) ตัวไหนใหม่จริง แล้วค่อย crux เฉพาะตัวใหม่ ดู [[findrepo]] skill ที่มี gate นี้อยู่แล้วแม้ไม่ได้เรียก skill ตรงๆ
  - **กฎถาวรจริงอยู่ที่ `F:\MD\README.md`** กฎข้อ 1 "Crux First Discovery & 3-Tier Search Protocol" (Tier 1 Master Catalog → Tier 2 mdกลาง Index → Tier 3 Web) — ที่นี่แค่ cross-link กันซ้ำ source of truth (one fact, one home) · README ยังมีกฎข้อ 5 ที่พลาดไปรอบนี้: เปิด session ใหม่ต้องอ่าน `CRUX_UNIFIED_MASTER_CATALOG.md` + `CURRENT_STATE.md` เป็น action แรกเสมอ ไม่ใช่แค่ grep ตอนมีลิงก์มา · และกฎข้อ 2 Auto-Sync: แก้ catalog ต้องรัน `generate_crux_unified_catalog.py` ครบ ไม่ใช่แก้บรรทัดเดียวพอ (เคยทำไม่ครบ 2026-10-16 — แก้ `CRUX_UNIFIED_MASTER_CATALOG.md` แต่ไม่ได้ sync `MASTER_SKILL_INDEX.md`/`ALL_REPOS_MASTER_INDEX.md`/`SKILL_TAXONOMY_ROUTER.md`/`CURRENT_STATE.md`)
  - **เช็คแล้ว (2026-10-16): ยังไม่มี SQL สำหรับ skill/repo catalog จริง** — มี SQLite เดียวที่ `F:\MD\systems\continuity-core\IDENTITY_REGISTRY.sqlite` แต่เป็น agent identity registry (table `agents`, 7 แถว) คนละเรื่อง — README เองบอกชัด (`KNOWLEDGE-MD-SQL-BRIDGE-001`): "ระหว่างยังไม่มี schema/authority อนุมัติ ให้ Markdown เป็น reference-only ห้ามสร้าง SQL แบบเดาสุ่ม" → Markdown ยังเป็น source of truth จนกว่าจะมีคนอนุมัติ schema จริง

- **เจอข้อมูลขัดแย้งกันระหว่างเอกสาร → ถามผู้ใช้ก่อนเสมอ ห้ามตัดสินเองแล้วแก้เงียบๆ:**
  - ผู้ใช้สั่งเป็นกฎถาวร 2026-10-16 หลัง agent เคยอ้าง `kb.md:145` ผิด (อ้างว่ามี record ที่จริงไม่มี) — บันทึกเป็น `CONFLICT-ASK-USER-001` ใน `F:\MD\README.md` rule 7
  - ข้อยกเว้น: มี ground-truth ชัดเจนอยู่แล้ว (grep นับแถวจริงเทียบ header ที่พิมพ์เลขผิด, คำสั่ง owner ที่บันทึกไว้แล้วเช่น A2A retirement) — แก้ตรงนี้ได้ทันทีเพราะเป็นการแก้ให้ตรง fact ไม่ใช่ตัดสินแทน owner
  - รายละเอียดเคสเต็ม + การแก้ที่ใช้กฎนี้รอบแรก → [[Key Decisions]] entry "mdกลาง/ai-shared consolidation 2026-10-16"
