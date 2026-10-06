# E-Nose Coffee Cloud

Sistem E-Nose berbasis Cloud IoT untuk analisis dan pemantauan aroma kopi secara real-time menggunakan ESP32-S3, Azure IoT Hub, Azure Functions, Cosmos DB, dan Web Dashboard.

## Struktur Repositori

Proyek ini terdiri dari komponen utama:

- **`.github/workflows/`**: 
  - `azure-static-web-apps-*.yml`: CI/CD pipeline otomatis untuk deploy Frontend ke Azure Static Web Apps.
  - `main.yml`: Pipeline otomatis untuk build & push Docker image Backend Rust ke Azure Container Registry (ACR).
- **`iot/`**: Firmware ESP32-S3 yang ditulis dalam Rust (`esp-idf-svc`), terhubung ke Wi-Fi dan Azure IoT Hub (MQTT), serta mendukung OTA update firmware.
- **`azurefunction/`**: Azure Functions berbasis Node.js untuk memproses event/telemetri dari Azure IoT Hub ke Azure Cosmos DB.
- **`enose_dashboard_progress/`**:
  - `package.json`: Modul pembantu.
  - `enose_dashboard_progress/`:
    - `backend/`: REST & WebSocket API server berbasis Rust (Axum) terhubung ke Azure Cosmos DB (default port: `8081`, dilengkapi `Dockerfile`).
    - `frontend/`: Web dashboard interaktif berbasis React & Vite dengan fitur visualisasi grafik real-time, export laporan PDF & Excel (`.xlsx`).
    - `esp32/`: Firmware alternatif Arduino C++ untuk pengujian dan sampling sensor.

## Prasyarat

- Rust & Cargo (Nightly/Espressif Toolchain untuk ESP32-S3, dan Rust toolchain untuk backend)
- Node.js (v18+) & npm
- Docker (opsional, untuk build container backend)
- Azure CLI / Azure Functions Core Tools
- Akun Azure dengan IoT Hub, Cosmos DB for NoSQL, Azure Container Registry, dan Static Web Apps

## Konfigurasi Lingkungan

Sebelum menjalankan komponen secara lokal, salin file contoh konfigurasi dan sesuaikan kredensial Anda:

1. **Azure Functions**:
   ```bash
   cd azurefunction
   cp local.settings.json.example local.settings.json
   ```
2. **Dashboard Backend**:
   ```bash
   cd enose_dashboard_progress/enose_dashboard_progress/backend
   cp .env.example .env
   ```

> **Catatan Keamanan**: Jangan pernah mempublikasikan file `.env` atau `local.settings.json` yang berisi kunci rahasia/connection string ke repositori publik.
