# ⬛ PixelForge

> Transform any photo into stunning pixel art — with AI-powered face detection.

A full-stack platform inspired by Kling AI, built with **Python (FastAPI)** backend and **React** frontend. Upload any image and convert it to colored pixel art with smart face awareness (keep faces sharp or pixelate them for privacy).

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔲 Pixel Art Engine | Convert any image to blocky pixel art (2–64px block size) |
| 🎨 Color Palettes | Game Boy, NES, Commodore 64, Cyberpunk, Pastel, Auto |
| 👤 Face Detection | OpenCV Haar cascade — protect or pixelate detected faces |
| 🖼️ Drag & Drop Upload | Direct upload from browser |
| ✨ AI Generation | Generate images from text prompt (requires OpenAI API key) |
| 📥 Download | Export final PNG with one click |
| 🔲 Grid Overlay | Optional pixel grid for that authentic retro look |

---

## 🗂️ Project Structure

```
pixelforge/
├── backend/
│   ├── main.py             # FastAPI server — all image processing logic
│   └── requirements.txt    # Python dependencies
├── frontend/
│   ├── public/index.html
│   └── src/
│       ├── index.js
│       └── App.jsx         # React UI
├── .env                    # Environment variables (DO NOT COMMIT)
├── .env.example            # Template — safe to commit
└── README.md
```

---

## 🚀 Quick Start

### 1. Clone / unzip the repo

```bash
unzip pixelforge.zip
cd pixelforge
```

### 2. Configure environment

```bash
cp .env.example .env
# Edit .env with your values (optional: add OPENAI_API_KEY for AI generation)
```

### 3. Start the Python backend

```bash
cd backend
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt
python main.py
# Server runs at http://localhost:8000
```

### 4. Start the React frontend

```bash
cd frontend
npm install
npm start
# App opens at http://localhost:3000
```

---

## ⚙️ Environment Variables

| Variable | Default | Description |
|---|---|---|
| `HOST` | `0.0.0.0` | Backend host |
| `PORT` | `8000` | Backend port |
| `DEBUG` | `False` | Reload on code change |
| `UPLOAD_DIR` | `uploads` | Where uploads are temporarily stored |
| `OUTPUT_DIR` | `outputs` | Where processed images are saved |
| `MAX_FILE_SIZE_MB` | `20` | Max upload size |
| `DEFAULT_PIXEL_SIZE` | `16` | Default block size |
| `OPENAI_API_KEY` | *(optional)* | Enables AI prompt → image → pixel pipeline |
| `STABILITY_API_KEY` | *(optional)* | Alternative: Stability AI generation |
| `SECRET_KEY` | — | Change before deploying to production |

---

## 🎨 Pixel Art Pipeline

```
Original Image
    │
    ▼
Color Quantization  ← reduces palette to N colors
    │
    ▼
Pixelation          ← downscale + upscale (nearest neighbor)
    │
    ▼
Face Detection      ← OpenCV Haar cascade
    │
    ├─ protect_faces=True  → restore sharp face region
    └─ protect_faces=False → apply heavier pixelation to faces
    │
    ▼
Palette Mapping     ← (optional) snap to preset palette
    │
    ▼
Grid Overlay        ← (optional) draw pixel grid lines
    │
    ▼
Output PNG
```

---

## 🔌 API Endpoints

| Method | Path | Description |
|---|---|---|
| `GET` | `/` | Health check |
| `GET` | `/palettes` | List available palette names |
| `POST` | `/upload` | Upload image file → base64 |
| `POST` | `/process` | Pixelate a base64 image |
| `POST` | `/generate-prompt` | Text → AI image → pixelate |
| `GET` | `/outputs/{filename}` | Download processed image |

### `/process` Request Body

```json
{
  "image_b64": "data:image/png;base64,...",
  "pixel_size": 16,
  "num_colors": 16,
  "protect_faces": true,
  "face_pixel_size": 8,
  "add_grid": false,
  "palette": "nes"
}
```

---

## 🛠️ Tech Stack

- **Backend**: Python 3.10+, FastAPI, Uvicorn, Pillow, OpenCV, NumPy
- **Frontend**: React 18, plain CSS-in-JS (no extra deps)
- **AI (optional)**: OpenAI DALL-E 3 via `openai` SDK

---

## 📝 License

MIT — use freely, attribution appreciated.
