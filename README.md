# DayZ Crime Clock — 5486 ASIA PACIFIC SG

เว็บแสดงข้อมูล player แบบ Live สำหรับเซิร์ฟ DayZ 5486 APAC Singapore

## วิธี Deploy บน GitHub Pages (ฟรี 100%)

### ขั้นตอน

**1. สร้าง Repository ใหม่บน GitHub**
- ไปที่ github.com → New repository
- ชื่อ repo: `dayz-crimeclock` (หรืออะไรก็ได้)
- ตั้งเป็น **Public**
- กด Create repository

**2. อัปโหลดไฟล์ทั้งหมด**
```
dayz-crimeclock/
├── .github/
│   └── workflows/
│       └── fetch-data.yml   ← GitHub Actions (หัวใจหลัก)
├── index.html               ← หน้าเว็บ
├── data.json                ← ข้อมูล server (auto-updated)
└── README.md
```

อัปโหลดผ่าน GitHub UI: ลาก-วางทุกไฟล์ หรือใช้ git push

**3. เปิด GitHub Pages**
- ไปที่ repo → Settings → Pages
- Source: **Deploy from a branch**
- Branch: **main** / folder: **/ (root)**
- กด Save

**4. เปิดใช้ GitHub Actions**
- ไปที่ repo → Actions
- ถ้ามี popup ถาม → กด "I understand my workflows, go ahead and enable them"

**5. รัน Actions ครั้งแรก**
- Actions → "Fetch DayZ Server Data" → Run workflow
- รอ 1-2 นาที → `data.json` จะอัปเดต

**6. เข้าเว็บ**
- URL: `https://[username].github.io/[repo-name]/`

---

## วิธีทำงาน

```
GitHub Actions (ทุก 5 นาที)
    ↓
curl https://api.battlemetrics.com/servers/4857562
    ↓
บันทึกเป็น data.json → git commit → push
    ↓
GitHub Pages เสิร์ฟ index.html + data.json
    ↓
Browser อ่าน data.json (ไม่มี CORS ปัญหา!)
```

ไม่มี server ไม่มีค่าใช้จ่าย รันตลอด 24 ชม. ฟรี!

---

## หมายเหตุ

- GitHub Actions ฟรี 2,000 นาที/เดือน (5 นาที × 288 ครั้ง/วัน × 30 วัน ≈ 720 นาที = ยังเหลือเยอะ)
- ข้อมูลอาจช้ากว่า real-time 0-5 นาที
- หาก Actions ไม่รัน: ตรวจสอบ repo → Actions → เปิดใช้งาน
