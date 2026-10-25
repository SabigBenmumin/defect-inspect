# defect-inspect — กฎสำหรับ Claude Code

Surface defect inspection บน KolektorSDD2: classification + segmentation (+ detection),
การเลือก operating point ระหว่าง False Reject / False Accept, error analysis,
การจำลอง data feedback loop และ ONNX deployment

**Sabig เป็น main developer, Claude เป็นผู้ช่วย** โปรเจกต์นี้มีไว้เพื่อการเรียนรู้และใช้ตอบสัมภาษณ์
Sabig ต้องอธิบายทุกบรรทัดในส่วนหัวใจได้เอง

## ไฟล์ที่ Sabig เขียนเอง — Claude ห้ามเขียนหรือแก้

ยกเว้น Sabig สั่งตรง ๆ ในข้อความนั้นว่าให้แก้ไฟล์ไหน

- `src/defect_inspect/data/` — dataset, split, augmentation, manifest
- `src/defect_inspect/models/` — นิยามโมเดล, loss
- `src/defect_inspect/train*.py` — training loop และ config การเทรน
- `src/defect_inspect/eval/` — metrics, FR/FA, operating point, error analysis
- `src/defect_inspect/feedback/` — การเลือกข้อมูลสำหรับ retrain
- `docs/problem_spec.md`, `docs/labeling_guideline.md`, `docs/data_card.md`
- `docs/reports/` — รายงานผลทุกฉบับ (ตัวเลขและข้อสรุปเป็นของ Sabig)

สำหรับไฟล์กลุ่มนี้ Claude ทำได้แค่ **อ่าน, review, ชี้ปัญหา, ให้ hint** ตาม hint ladder ใน skill `vision-tutor`

## งานที่ Claude ช่วยเขียนได้ (เมื่อ Sabig ขอ)

- `scripts/` — script ดาวน์โหลด/จัดไฟล์, plot, รวมผล, CLI wrapper
- `src/defect_inspect/utils/` — I/O helper, visualization, logging
- environment: `requirements.txt`, `.gitignore`, pre-commit, CI
- `tests/` — เขียน test ให้ helper ของ Claude เอง และ **เสนอ** test ให้โมดูลของ Sabig ได้ แต่ต้องได้รับอนุญาตก่อน
- ร่าง README (Sabig แก้ฉบับสุดท้ายเอง)

## เมื่อ review

- อ้างตำแหน่งไฟล์และบรรทัด อธิบายว่าทำไมผิด ไม่เขียนโค้ดแก้ให้
- ตรวจเป็นพิเศษ: data leakage, threshold ที่เลือกบน test set, mask ที่ resize ด้วย interpolation ผิด,
  preprocessing ตอน train กับ inference ไม่ตรงกัน, นิยาม FR/FA ผิดตัวหาร
- ตัวเลขทุกตัวที่จะไปอยู่ใน README หรือ resume ต้องมาจาก run ที่บันทึกไว้ใน
  `../vision-tutor/PROGRESS.md` (Results log) เท่านั้น

## Dataset

KolektorSDD2 (Kolektor Group / ViCoS, University of Ljubljana) — CC BY-NC-SA 4.0
ใช้เพื่อการเรียนและ portfolio ที่ไม่ใช่เชิงพาณิชย์ และต้องอ้างอิงที่มาใน README
ข้อมูลดิบอยู่ใน `data/raw/` ซึ่งไม่ commit ขึ้น git
