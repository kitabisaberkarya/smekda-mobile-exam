# 📱 ExamBrowser - Aplikasi Ujian Digital Aman

Aplikasi ujian digital berbasis Flutter untuk Android dengan fitur keamanan tinggi.

## ✨ Fitur

- 🔒 **Lock Layar** — Tidak bisa keluar dari app saat ujian berlangsung
- 📵 **Blokir Screenshot** — Layar tidak bisa di-screenshot/screen record
- 📡 **Soal dari Server** — Soal diambil secara real-time dari server
- ⏱️ **Timer Otomatis** — Ujian otomatis dikumpulkan saat waktu habis
- 🗂️ **Navigasi Soal** — Grid navigasi antar soal
- ✅ **Auto Submit** — Jawaban terkirim otomatis ke server

---

## 🚀 Cara Deploy (Auto Build APK via GitHub)

### Langkah 1: Upload ke GitHub
```bash
git init
git add .
git commit -m "Initial ExamBrowser"
git branch -M main
git remote add origin https://github.com/USERNAME/exam-browser.git
git push -u origin main
```

### Langkah 2: APK Otomatis di-build
Setelah push, GitHub Actions akan otomatis:
1. Install Flutter
2. Build APK debug & release
3. Upload ke tab **Releases** di GitHub

### Langkah 3: Download APK
Buka: `https://github.com/USERNAME/exam-browser/releases`

---

## ⚙️ Konfigurasi Server

Edit file `lib/services/api_service.dart`:

```dart
static const String baseUrl = 'https://your-server.com/api';
```

### Format API Response (GET /exam/{code})
```json
{
  "id": "exam-001",
  "title": "Ujian Matematika Semester 1",
  "subject": "Matematika",
  "duration_minutes": 90,
  "student_name": "Budi Santoso",
  "questions": [
    {
      "number": 1,
      "text": "Berapakah hasil dari 2 + 2?",
      "type": "multiple_choice",
      "options": ["2", "4", "6", "8"]
    },
    {
      "number": 2,
      "text": "Jelaskan teorema Pythagoras!",
      "type": "essay"
    }
  ]
}
```

### Format Submit (POST /exam/submit)
```json
{
  "exam_id": "exam-001",
  "answers": {
    "0": "B",
    "1": "Teorema Pythagoras menyatakan..."
  },
  "submitted_at": "2024-01-15T10:30:00Z"
}
```

---

## 🛠️ Development Lokal

```bash
# Install dependencies
flutter pub get

# Run di emulator/device
flutter run

# Build APK manual
flutter build apk --release
```

---

## 📁 Struktur Project

```
exam_browser/
├── .github/workflows/
│   └── build-apk.yml          # GitHub Actions (auto build APK)
├── lib/
│   ├── main.dart               # Entry point
│   ├── models/
│   │   └── exam_model.dart     # Data models
│   ├── services/
│   │   ├── api_service.dart    # HTTP calls ke server
│   │   └── exam_provider.dart  # State management
│   └── screens/
│       ├── login_screen.dart   # Halaman login ujian
│       ├── exam_screen.dart    # Halaman ujian (aman)
│       └── result_screen.dart  # Halaman hasil
├── android/
│   └── app/src/main/
│       └── AndroidManifest.xml # Android permissions
└── pubspec.yaml                # Flutter dependencies
```
