# ReflectBot

ReflectBot adalah chatbot refleksi diri berbasis Flask yang menganalisis pola kelekatan (attachment style) seseorang dari percakapan chat menggunakan IndoBERT dan model machine learning lokal, lalu memberikan wawasan empatik melalui Google Gemini API.

## Fitur

- Autentikasi pengguna (login/register) dengan Flask-Login dan Flask-Bcrypt
- Ruang chat interaktif dengan engine percakapan berbasis intent classification
- Deteksi intent: greeting, sharing emotion, attachment anxious, attachment avoidant, self reflection, closure, general
- Analisis gaya kelekatan (secure / anxious / avoidant) dengan IndoBERT + Gradient Boosting
- Ekstraksi frasa kunci dan skor TF-IDF
- Statistik teks dan fitur BERT (embedding)
- Analisis AI insights dan penjelasan frasa melalui Google Gemini (`gemini-2.0-flash-exp`)
- Simpan sesi chat dan hasil analisis ke database
- Tampilan frontend dengan Bootstrap

## Teknologi

- Python, Flask, Flask-SQLAlchemy, Flask-Login, Flask-Bcrypt
- IndoBERT (`indobenchmark/indobert-base-p1`) via Hugging Face Transformers
- Gradient Boosting model (lokal, `.pkl`)
- Sastrawi (stopword removal & stemming untuk Bahasa Indonesia)
- Google Gemini API (`google-genai`)
- SQLAlchemy (SQLite atau MySQL)
- JavaScript, Bootstrap 5

## Struktur Project

```
reflectbot-main/
├── app.py                      # Entry point Flask (sederhana)
├── main.py                     # Entry point Flask (factory)
├── requirements.txt            # Dependensi Python
├── .env.example                # Template variabel lingkungan
├── .gitignore
├── README.md
├── app/
│   ├── __init__.py             # Aplikasi Flask & konfigurasi DB
│   ├── models.py               # Model database (User, ChatSessions, ChatMessages, SessionAnalysis)
│   ├── auth.py                 # Login, register, logout
│   ├── views.py                # Halaman utama & daftar sesi
│   ├── chat_session.py         # Manajemen sesi chat
│   ├── chat_message.py         # Kirim pesan, analisis percakapan, explain phrase
│   ├── chatbot_service.py      # Prediksi attachment style (IndoBERT + GB)
│   ├── genai_analyzer.py       # Analisis AI dengan Google Gemini
│   ├── intent_classifier.py    # Intent classifier & conversation engine
│   ├── model/                  # Model & scaler yang sudah dilatih (.pkl, .json)
│   ├── routes/                 # Blueprint routes
│   ├── static/                 # CSS, JS, gambar
│   └── templates/              # HTML templates
```

## Instalasi

### 1. Clone repository

```bash
git clone https://github.com/Rafaellie/reflectbot.git
cd reflectbot
```

### 2. Buat environment virtual (opsional tapi disarankan)

```bash
python -m venv venv
venv\Scripts\activate   # Windows
# atau
source venv/bin/activate  # Linux/Mac
```

### 3. Install dependensi

```bash
pip install -r requirements.txt
```

### 4. Konfigurasi environment

Salin file contoh:

```bash
copy .env.example .env   # Windows
# atau
cp .env.example .env     # Linux/Mac
```

Edit file `.env` dan isi nilai yang sesuai:

```env
SECRET_KEY=ganti-dengan-kunci-rahasia-anda
DATABASE_URL=sqlite:///app.db
GEMINI_API_KEY=ganti-dengan-api-key-gemini-anda
```

- `SECRET_KEY`: Kunci rahasia Flask untuk session security.
- `DATABASE_URL`: Gunakan `sqlite:///app.db` untuk SQLite (default, mudah), atau MySQL jika diinginkan.
- `GEMINI_API_KEY`: Dapatkan dari https://aistudio.google.com/app/apikey

### 5. Jalankan aplikasi

```bash
python main.py
```

Aplikasi akan berjalan di `http://localhost:5000`.

## Cara Penggunaan

1. Register atau login sebagai pengguna
2. Buat sesi chat baru
3. Obrolan dengan ReflectBot tentang perasaan atau hubungan Anda
4. Klik tombol "Analisis Percakapan" untuk melihat hasil analisis gaya kelekatan
5. Lihat ringkasan AI dan penjelasan frasa kunci

## Lisensi

Projek ini dikembangkan untuk keperluan pembelajaran / penelitian.
