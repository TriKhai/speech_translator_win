# Speech Translator

Ứng dụng desktop **nhận dạng giọng nói, phiên âm và dịch thuật** theo thời gian thực, hỗ trợ ghi âm cuộc họp và nhận diện nhiều người nói. Xây dựng bằng Python + PyQt6.

---

## Tính năng

- **Nhận dạng giọng nói (ASR)** — sử dụng Whisper (faster-whisper / CTranslate2) và Wav2Vec2
- **Dịch thuật tự động** — hỗ trợ nhiều ngôn ngữ qua deep-translator
- **Speaker Diarization** — nhận diện và phân biệt nhiều người nói
- **Ghi lại cuộc họp** — tự động tạo biên bản, tóm tắt và mind map
- **Upload file audio** — xử lý file âm thanh có sẵn
- **Lịch sử phiên** — lưu trữ và tìm kiếm lại các buổi ghi âm
- **Xuất file** — hỗ trợ export transcript ra nhiều định dạng
- **Giao diện desktop** — UI hiện đại với PyQt6

---

## Yêu cầu hệ thống

- Python **3.10**
- Windows 10/11 (có hỗ trợ build `.exe` qua PyInstaller)
- Microphone hoặc file audio
- Máy có CPU càng yếu thì càng lag

---

## Cài đặt

### 1. Clone repository

```bash
git clone https...
cd speech-translator
```

### 2. Tạo môi trường ảo

```bash
python -m venv venv
venv\Scripts\activate      # Windows
# hoặc
source venv/bin/activate   # Linux/macOS
```

### 3. Cài đặt dependencies

```bash
pip install -r requirements.txt
```

> Một số package như `PyAudio`, `sounddevice` có thể cần cài thêm driver âm thanh trên Windows. Nếu gặp lỗi, thử cài thủ công:
> ```bash
> pip install PyAudio sounddevice
> ```

### 4. Cấu hình biến môi trường

Tạo file `.env` ở thư mục gốc:

```env
GROQ_API_KEY=your_groq_api_key_here
```

> Lấy API key miễn phí tại [console.groq.com](https://console.groq.com)

### 5. Chạy ứng dụng

```bash
python main.py
```

---

## Cấu trúc thư mục

```
speech-translator/
├── main.py                  # Entry point
├── core/                    # Logic xử lý âm thanh & AI
│   ├── whisper_service.py   # ASR với Whisper
│   ├── translation_service.py
│   ├── speaker_diarizer.py  # Nhận diện người nói
│   ├── meeting_capture.py   # Ghi cuộc họp
│   └── summary_service.py   # Tóm tắt tự động
├── ui/                      # Giao diện PyQt6
│   ├── main_window.py
│   └── pages/               # Các trang: Live, Meeting, Upload, History...
├── db/                      # Database (SQLAlchemy)
├── models/                  # Whisper models local
└── .env                     # Biến môi trường (không commit)
```

---

## Build file .exe (Windows)

```bash
pyinstaller --onedir  --add-data "...\venv\lib\site-packages\resemblyzer;resemblyzer"  --add-data "...\venv\lib\site-packages\silero_vad;silero_vad"  --add-data "dialogue_categories.json;."  main.py
```

File `.exe` sẽ được tạo trong thư mục `dist/`.

Nhớ chỉnh lại path của bạn.

---
