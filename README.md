# Goergenexus School — Onlayn Təhsil Platforması

Goergenexus School, 9–12-ci siniflər üçün ABŞ standartlarına uyğun onlayn təhsil platformasıdır. OpenStax açıq dərslikləri, tələbə kabineti, müəllim paneli və real-time irəliləyiş izləməsi ilə təchiz olunmuşdur.

## 🎯 Xüsusiyyətlər

- ✅ Tələbə qeydiyyatı və autentifikasiyası (Firebase)
- ✅ Tələbə şəxsi kabineti (progress tracking, dərs siyahısı)
- ✅ Müəllim/Admin paneli (kurs idarəetməsi, tələbə idarəetməsi)
- ✅ OpenStax 9–12 dərslikləri (16+ fənn)
- ✅ Dərs tamamlama və qiymətləndirmə sistemi
- ✅ Azərbaycan dili dəstəyi
- ✅ Mobil uyğun dizayn
- ✅ E-poçt bildirişləri

## 📁 Layihə Struktur

```
goergenexus-school/
├── index.html              # Ana sayt (landing page)
├── curriculum.html         # Dərslik kataloqu
├── admin.html              # Müəllim paneli
├── server.js               # Express backend
├── package.json            # Node.js dependencies
├── vercel.json             # Vercel deploy config
├── .env.example            # Environment variables şablonu
└── .gitignore              # Git ignore
```

## 🚀 Sürətli Başlanğıc

### 1️⃣ GitHub-dan klonla

```bash
git clone https://github.com/globalnexus-max/goergenexus-school.git
cd goergenexus-school
```

### 2️⃣ Firebase Layihəsi Yarat

1. [Firebase Console](https://console.firebase.google.com/) açıl
2. **Yeni Layihə** ➜ "goergenexus-school"
3. **Firestore Database** aktiv et (Production Mode)
4. **Authentication** açıl ➜ Email/Password dəstəyini aç
5. **Layihə Tənzimləri** ➜ Service Account Key indir (JSON)

### 3️⃣ Environment Variables Tənzimləməsi

`.env` faylı yarat:

```env
FIREBASE_SERVICE_ACCOUNT={"type":"service_account","project_id":"your-project-id",...}
FIREBASE_DATABASE_URL=https://your-project.firebaseio.com
JWT_SECRET=your-super-secret-jwt-key-here-min-32-chars
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-gmail-app-password
CLIENT_URL=http://localhost:3000
PORT=5000
NODE_ENV=development
```

### 4️⃣ Backend Quraş

```bash
npm install
npm run dev  # Development modunda başla (localhost:5000)
```

### 5️⃣ Frontend İstifadə Etmək

- Ana sayt: `http://localhost:3000`
- Admin paneli: `http://localhost:3000/admin.html`

## 🔐 Autentifikasiya

### Qeydiyyat
```javascript
POST /api/auth/register
{
  "email": "student@example.com",
  "password": "secure-password",
  "name": "Aysel Məmmədova",
  "grade": 9
}
```

### Giriş
```javascript
POST /api/auth/login
{
  "email": "student@example.com",
  "password": "secure-password"
}
```

Response:
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "uid": "user-id",
    "email": "student@example.com",
    "name": "Aysel Məmmədova",
    "grade": 9
  }
}
```

## 📚 API Endpoints

### Tələbə Routes

| Method | Endpoint | Təsvir |
|--------|----------|--------|
| POST | `/api/auth/register` | Qeydiyyat |
| POST | `/api/auth/login` | Giriş |
| GET | `/api/user/profile` | Profili əldə et |
| PUT | `/api/user/profile` | Profili güncəllə |
| GET | `/api/courses/:grade` | Sinif kurslarını əldə et |
| GET | `/api/courses/:courseId/lessons` | Kursun dərsləri |
| POST | `/api/lessons/:lessonId/complete` | Dərsi tamamla |
| GET | `/api/user/progress` | İrəliləyişi əldə et |

### Admin Routes

| Method | Endpoint | Təsvir |
|--------|----------|--------|
| GET | `/api/admin/users` | Bütün tələbələr |
| POST | `/api/admin/courses` | Yeni kurs yarat |
| POST | `/api/admin/courses/:courseId/lessons` | Yeni dərs əlavə et |

## 🗄️ Firestore Struktur

```
users/
├── {uid}
│   ├── email: "student@example.com"
│   ├── name: "Aysel"
│   ├── grade: 9
│   ├── createdAt: timestamp
│   └── progress/
│       ├── {lessonId}
│       │   ├── completedAt: timestamp
│       │   └── status: "completed"

courses/
├── {courseId}
│   ├── title: "English Language Arts"
│   ├── grade: 9
│   ├── subject: "English"
│   └── lessons/
│       ├── {lessonId}
│       │   ├── title: "Lesson 1"
│       │   ├── content: "HTML content"
│       │   ├── order: 1
│       │   └── videoUrl: "https://..."
```

## 🌐 Vercel-ə Deploy

### 1. Vercel Hesabı Yarat

[Vercel.com](https://vercel.com) → Sign up (GitHub ilə)

### 2. Layihəni Bağla

```bash
vercel --prod
```

### 3. Environment Variables Tənzimləməsi

Vercel Dashboard → Layihə → Settings → Environment Variables:
- `FIREBASE_SERVICE_ACCOUNT`
- `FIREBASE_DATABASE_URL`
- `JWT_SECRET`
- `EMAIL_USER`
- `EMAIL_PASSWORD`
- `CLIENT_URL` (production URL)

### 4. Deploy Edin

```bash
vercel --prod
```

**Sayt URL:** `https://goergenexus-school.vercel.app`

## 👨‍🏫 Müəllim Panel Əsasları

1. **Admin Hesabı Yarat:**
   - Firebase Console → Authentication
   - Manual email/password ilə yeni istifadəçi əlavə et
   - Firestore-da `role: "admin"` tənzimləyin

2. **Admin Panelə Daxil Ol:**
   - `/admin.html` açıl
   - Admin emailini əldə et
   - Dashboard → Kurslar → Yeni Kurs

3. **Kurs Yaratmaq:**
   - Kurs adı və təsviri
   - Sinif səviyyəsi (9–12)
   - Fənn

4. **Dərs Əlavə Etmək:**
   - Kursda → Dərslər
   - Dərs adı, HTML məzmunu, video URL
   - Sıra nömrəsi

## 📱 Mobil Support

- Responsive dizayn (mobil + tablet + desktop)
- Touch-friendly buttons
- Adaptive navigation

## 🔒 Təhlükəsizlik

- JWT token-based auth
- Firebase Security Rules
- Environment variables ilə secret keylər
- CORS protection
- Password hashing (bcryptjs)

## 📞 Support & Tövsiyyələr

- Issue yarat: [GitHub Issues](https://github.com/globalnexus-max/goergenexus-school/issues)
- E-poçt: support@goergenexus.school

## 📄 Lisenziya

GNU General Public License v3.0 — [LICENSE](LICENSE) faylına bax

---

**Versiya:** 1.0.0  
**Yaradılış:** 2026  
**Təhsil Platforması:** Goergenexus School
