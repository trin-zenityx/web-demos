# PLAN — Pro Rollout: อัพเกรด 20 ระบบที่เหลือให้ระดับ production

อัพเดท: 2026-09-14 · สถานะรวม: Pro แล้ว 4/24 (POS, KDS, Queue, CRM)

## กฎเหล็ก (ทุกระบบ Pro ต้องผ่าน)
1. Entry pattern ไม่ซ้ำ (ดู Entry Matrix ด้านล่างใน PLAN-systems.md)
2. โลโก้จริงจาก AI (2 เครดิต) + ภาพ login/hero ถ้า pattern ต้องการ (3 เครดิต)
3. เขียน event ลง bridge `zx-link-v1` + feed drawer อ่านระบบอื่น
4. ไม่มี emoji ใน UI · ไอคอน SVG · tabular-nums
5. splash boot + offline pill + shortcuts + reset ข้อมูล
6. `?app=1` ข้าม entry เข้าแอปตรง
7. เทส CDP จริง (คลิก flow ครบ) + thumbnail หน้าแอป + อัพเดทการ์ด hub + push + live check
8. เขียนไฟล์เดียว index.html จบ · localStorage `zx-<name>2-v1`

## งบโควต้า (Kimi 5h rolling window)
- Tier S (rebuild ใหญ่ 60-100KB): 1 ระบบ/window — ผู้ช่วยเขียนเอง
- Tier A (rebuild กลาง): 1-2 ระบบ/window
- Tier B (light-touch): 3-4 ระบบ/window — มอบ subagent ได้ (brief แน่น)
- ถ้าโดน 403: หยุด รอ window ถัดไป ห้าม re-dispatch ซ้ำทันที

---

## Tier S — Full Pro (6 ระบบ · 6 windows)
| # | ระบบ | Entry | Signature features | Bridge events |
|---|---|---|---|---|
| 1 | inventory สต็อกดี | สแกนบัตรพนักงาน (เส้นสแกนวิ่ง) | รับ/เบิกจริง ตัดสต็อก POS สะท้อน, low-stock alert, PO แนะนำสั่งซื้อ, movement log | stock-in/stock-out/stock-low |
| 2 | documents เอกสารดี | เลือก workspace บริษัท | QT→IV→RE chain แปลงเอกสาร, VAT 7%, พิมพ์ A4 จริง, เลขที่รัน, ลายเซ็น/ตราประทับ | doc-issued/doc-paid |
| 3 | dashboard ผู้บริหารดี | ไม่มี gate "เดโมสด" | ดึงยอดขาย POS จาก bridge จริง, KPI live, กราฟหลายชุด, export CSV | (อ่านอย่างเดียว) |
| 4 | hr คนดี | เช็คอินใบหน้าจำลอง (กรอบสแกน) | ลงเวลาเข้า-ออก, OT, ใบลาอนุมัติ 2 ชั้น, สลิปเงินเดือน PDF | checkin/leave-approved |
| 5 | dorm ห้องดี | เลือกตึก/ห้อง (grid picker) | ผังห้อง, มิเตอร์น้ำไฟ→บิลอัตโนมัติ, แจ้งซ่อม, พิมพ์ใบเสร็จห้อง | bill-issued/repair-ticket |
| 6 | appointments นัดดี | การจอง = entry (flow จองเลย) | ปฏิทิน+slot จริง, เตือนล่วงหน้า, no-show, ปฏิทินหมอ/ช่างหลายคน | booking-new/booking-done |

## Tier A — Medium Pro (7 ระบบ)
| # | ระบบ | Entry | Signature |
|---|---|---|---|
| 7 | school เรียนดี | การ์ดนักเรียน/ครู แตะบัตร | เช็คชื่อสด, เกรด, ตารางเรียน |
| 8 | gym-members ฟิตดี | แตะบัตรสมาชิก QR | เช็คอิน, แพ็กเกจหมดอายุ, เทรนเนอร์ |
| 9 | repair ซ่อมดี | ลูกค้าแจ้งซ่อม/ช่าง (kiosk split) | ใบรับซ่อม, สถานะไหล, ประเมินราคา |
| 10 | hotel พักดี | front-desk/guest split | ผังห้อง check-in/out, คืนเงินมัดจำ |
| 11 | laundry-ops ซักดี | ชั่ง กก. เป็น entry | งานด่วน +30%, ตั๋วซัก, สถานะเครื่อง |
| 12 | purchasing จัดซื้อดี | เลือกบทบาท (ผู้ขอ/ผู้อนุมัติ) | PR→PO approve flow, งบคงเหลือ |
| 13 | loyalty แต้มดี | สแกนสมาชิก | แต้มจาก POS bridge จริง, แลกของรางวัล |

## Tier B — Light-touch (7 ระบบ · subagent ได้)
kanban งานดี, admin-shop ร้านดีแอดมิน, cashbook เงินดี, sales-report ยอดขายดี, delivery ส่งดี, rental เช่าดี, tournament แข่งดี
> scope: ขัด UI ให้เทียบชุด Pro, ลบ emoji, entry ไม่ซ้ำ (เลือกจาก matrix), bridge event 1-2 ตัว, seed สมจริง, thumbnail ใหม่

---

## Progress log
- [x] POS ขายดี v2.5 (2026-09-13)
- [x] KDS ครัวดี (2026-09-14)
- [x] Queue คิวดี (2026-09-14)
- [x] CRM ลูกค้าดี (2026-09-14)
- [x] Inventory สต็อกดี (2026-09-14 · badge-scan entry, ROP+PO, POS bridge sales feed)
- [x] Documents เอกสารดี (2026-09-14 · workspace picker, QT→IV→RE chain, baht text, CRM→IV bridge)
- [x] Dashboard ผู้บริหารดี (2026-09-15 · no-gate live command center, รวม bridge 6 ระบบ)
- [x] HR คนดี (2026-09-15 · face-scan check-in, สาย/OT, ใบลา 2 ชั้น, payroll จริง)
- [x] Dorm ห้องดี (2026-09-15 · ผังห้องเป็น entry, มิเตอร์→บิล, ใบเสร็จพิมพ์)
- [x] Appointments นัดดี (2026-09-15 · booking-first entry, slot collision, walk-in) — **Tier S ครบ 6/6**
- [x] School เรียนดี (2026-09-15 · card-tap entry + bell, roll call, grades)
- [x] Gym ฟิตดี (2026-09-15 · QR member scan = check-in, expired block, renew, class booking)
- [ ] (ว่าง — Tier A ตัวถัดไป: repair)
