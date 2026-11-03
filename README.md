# Circulation Desk (ฉบับตั้งต้นสำหรับนักศึกษา)

ระบบยืม-คืนหนังสือของห้องสมุดขนาดเล็ก (PHP + MySQL/MariaDB) ใช้ประกอบรายวิชา 5672603 การจัดการโครงแบบซอฟต์แวร์

คลังนี้มีเพียงไฟล์ตั้งต้นส่วนน้อย นักศึกษาจะเพิ่มส่วนที่เหลือเองผ่าน Git และ GitHub ตามปฏิบัติการในแต่ละบท

## ไฟล์ที่มีให้

| ไฟล์ | หน้าที่ |
|---|---|
| `docs/01-project-charter-and-requirements.md` | กฎบัตรโครงการ ความต้องการ R-01 ถึง R-08 และกฎธุรกิจ BR-01 ถึง BR-04 |
| `db/init/01-schema.sql` | โครงสร้างฐานข้อมูล 5 ตาราง (Schema 1.0.0) |
| `src/config/config.php` | ค่าตั้งระบบ อ่านจากตัวแปรสภาพแวดล้อมหรือ `config.local.php` |
| `src/config/config.local.example.php` | แม่แบบค่าเฉพาะเครื่อง (คัดลอกเป็น `config.local.php`) |
| `.env.example` | แม่แบบตัวแปรสภาพแวดล้อมสำหรับ Docker (คัดลอกเป็น `.env`) |
| `.gitignore` | ไฟล์ที่ห้ามนำเข้าคลัง |

## สิ่งที่นักศึกษาต้องเพิ่ม

- เอกสาร: รายการ SCI และกติกาการตั้งชื่อ, ER และสถาปัตยกรรม, BUILD.md, ทะเบียน Change Request, Traceability Matrix
- ฐานข้อมูล: ข้อมูลตัวอย่าง `db/init/02-seed.sql`
- โค้ด: `src/lib/`, `src/services/`, `src/views/` และหน้าเว็บใน `src/public/` ตาม R-01 ถึง R-08
- สภาพแวดล้อม: `docker-compose.yml` และ `docker/php/Dockerfile`
- ชุดทดสอบใน `tests/`

## เริ่มต้นใช้งาน

```bash
git clone https://github.com/SiyaphatLPRU/-Uncompleted-CirculationDesk.git
cd -- -Uncompleted-CirculationDesk
git switch -c feature/R-01-login
# เพิ่มหรือแก้ไฟล์
git add <ไฟล์>
git commit -m "feat(auth): add login page" -m "Refs: R-01"
git push -u origin feature/R-01-login
```

จากนั้นเปิด Pull Request เข้า `main` ให้เพื่อน Review ก่อน Merge และใช้ `git pull` ดึงงานล่าสุดก่อนเริ่มงานใหม่ทุกครั้ง

## กติกาสำคัญ

- ห้ามแก้บน `main` โดยตรง ทุกงานต้องผ่าน Branch และ Pull Request
- ชื่อ Branch: `feature/R-xx-<สั้น>`, `fix/<สั้น>`, `docs/<สั้น>`
- ข้อความ Commit: `<ชนิด>(<ขอบเขต>): <สรุป>` และบรรทัด `Refs: R-xx` (ชนิด: feat, fix, docs, test, refactor, style, chore)
- ห้าม commit `.env` และ `src/config/config.local.php` เพราะมีรหัสผ่านจริง
- ห้ามแก้ `db/init/01-schema.sql` เมื่อออก Baseline แล้ว ให้เพิ่มไฟล์ migration ใหม่ เช่น `db/init/03-...sql`
