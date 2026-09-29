# E-Nose Coffee Cloud

Sistem E-Nose berbasis Cloud IoT untuk analisis dan pemantauan aroma kopi secara real-time menggunakan ESP32-S3, Azure IoT Hub, Azure Functions, Cosmos DB, dan Web Dashboard.

## Struktur Repositori

Proyek ini terdiri dari 3 komponen utama:

- **`iot/`**: Firmware ESP32-S3 yang ditulis dalam Rust (`esp-idf-svc`), terhubung ke Wi-Fi dan Azure IoT Hub (MQTT), serta mendukung OTA update firmware.
- **`azurefunction/`**: Azure Functions berbasis Node.js untuk memproses event/telemetri dari Azure IoT Hub ke Azure Cosmos DB.
- **`enose_dashboard_progress/`**:
  - `backend/`: REST & WebSocket API server berbasis Rust (Axum) terhubung ke Azure Cosmos DB.
  - `frontend/`: Web dashboard interaktif berbasis React & Vite.
  - `esp32/`: Firmware alternatif Arduino C++ untuk pengujian dan sampling sensor.

## Prasyarat

- Rust & Cargo (Nightly/Espressif Toolchain untuk ESP32-S3)
- Node.js (v18+) & npm
- Azure CLI / Azure Functions Core Tools
- Akun Azure dengan IoT Hub & Cosmos DB for NoSQL

## Konfigurasi Lingkungan

Sebelum menjalankan komponen, salin file contoh konfigurasi dan sesuaikan kredensial Anda:

1. **Azure Functions**:
   ```bash
   cd azurefunction
   cp local.settings.json.example local.settings.json
   ```
2. **Dashboard Backend**:
   ```bash
   cd enose_dashboard_progress/backend
   cp .env.example .env
   ```

> **Catatan Keamanan**: Jangan pernah mempublikasikan file `.env` atau `local.settings.json` yang berisi kunci rahasia/connection string ke repositori publik.
