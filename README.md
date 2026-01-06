# 🔋 Enerlytics v0.1 - Energy Monitoring & Management System

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15.x-336791?logo=postgresql)](https://www.postgresql.org/)
[![MQTT](https://img.shields.io/badge/MQTT-v3.1.1-660066)](https://mqtt.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Enerlytics** is an open-source, real-time energy monitoring and management system designed for industrial facilities and commercial businesses. Built with IoT devices (ESP32), it provides cost-effective energy tracking, AI-powered savings recommendations, and comprehensive reporting—all at **99% lower cost** than commercial solutions.

---

## 🌟 Key Features

- ⚡ **Real-Time Monitoring** - Live energy consumption tracking via ESP32 IoT devices
- 📊 **Advanced Analytics** - Historical data analysis and consumption predictions
- 🤖 **AI-Powered Recommendations** - Google Gemini API integration for intelligent savings tips
- 📈 **Comprehensive Reporting** - 6 report types (Device, Z-Report, Budget, Intensity, Green Energy, AI Analysis)
- 🔐 **Secure** - BCrypt password hashing, role-based access control
- 💰 **Cost-Effective** - Open-source alternative to $15K-$50K commercial systems
- 🌐 **MQTT Protocol** - Reliable IoT communication with QoS 1 and Last Will Testament
- 📱 **Modern UI** - DevExpress WinForms with real-time charts and dashboards

---

## 🏗️ Architecture

```
┌─────────────────────────────────────┐
│   ESP32 IoT Devices (Sensors)      │
│   • ACS712 (Current Sensor)         │
│   • ZMPT101B (Voltage Sensor)       │
└──────────────┬──────────────────────┘
               │ MQTT Protocol
┌──────────────▼──────────────────────┐
│      MQTT Broker (Mosquitto)        │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  Backend (.NET 8.0 + PostgreSQL)    │
│  • Layered Architecture             │
│  • Dapper ORM                       │
│  • Business Logic                   │
│  • Gemini AI Integration            │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  WinForms UI (DevExpress)           │
│  • Real-time Dashboard              │
│  • Device Management                │
│  • Report Generation                │
└─────────────────────────────────────┘
```

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|------------|
| **IoT** | ESP32, MQTT, ACS712, ZMPT101B |
| **Backend** | C# 12.0, .NET 8.0, Dapper ORM |
| **Database** | PostgreSQL 15.x, JSONB |
| **UI** | DevExpress WinForms, XtraCharts |
| **AI** | Google Gemini 1.5 Flash API |
| **Security** | BCrypt (Work Factor: 12) |
| **Messaging** | Eclipse Mosquitto 2.x |

---

## 📦 Installation

### Prerequisites

- **Windows 10/11** (64-bit)
- **.NET 8.0 Desktop Runtime** ([Download](https://dotnet.microsoft.com/download/dotnet/8.0))
- **PostgreSQL 15.x** ([Download](https://www.postgresql.org/download/))
- **Eclipse Mosquitto** ([Download](https://mosquitto.org/download/))
- **DevExpress 23.x** (Evaluation or Licensed)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/umutzaif/Enerlytics-Factory-Energy-Viewer.git
   cd Enerlytics-Factory-Energy-Viewer
   ```

2. **Database Setup**
   ```bash
   # Create database
   createdb -U postgres energymonitordb
   
   # Run schema scripts
   psql -U postgres -d energymonitordb -f schema_v2.sql
   psql -U postgres -d energymonitordb -f schema_v2_sps.sql
   ```

3. **Configure Connection String**
   
   Update `appsettings.json` in `EnergyMonitor.Launcher`:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Host=localhost;Database=energymonitordb;Username=postgres;Password=yourpassword"
     }
   }
   ```

4. **Start MQTT Broker**
   ```bash
   mosquitto -c mosquitto.conf
   ```

5. **Build & Run**
   ```bash
   cd EnergyMonitor.Launcher
   dotnet run
   ```

---

## 🚀 Quick Start

### 1. Login
- **Default Admin:** `admin` / `admin123`
- **Default Operator:** `operator` / `operator123`

### 2. Add IoT Device
1. Navigate to **Device Management**
2. Click **Add Device**
3. Enter device details (Name, MAC Address, etc.)
4. Save

### 3. Start Monitoring
- ESP32 devices automatically send data via MQTT
- Dashboard updates in real-time
- View live charts and metrics

### 4. Generate Reports
1. Go to **Reports** → **Report Filters**
2. Select date range and devices
3. Choose report type
4. Click **Generate PDF**

---

## 📊 Performance Metrics

| Metric | Target | Achieved | Status |
|--------|--------|----------|--------|
| **Functional Tests** | 95% | 98% | ✅ |
| **Query Performance** | <1s | 250ms | ✅ |
| **MQTT Data Loss** | <5% | <1% | ✅ |
| **Code Quality (McCabe)** | <10 | 6.8 | ✅ |
| **Cost Savings** | - | 99%+ | ✅ |

---

## 🔐 Security Features

- **BCrypt Password Hashing** (Work Factor: 12)
- **Role-Based Access Control** (Admin, Operator)
- **SQL Injection Protection** (Parameterized queries via Dapper)
- **MQTT Authentication** (Username/Password)
- **Future:** TLS/SSL encryption for MQTT

---

## 📸 Screenshots

### Dashboard
![Dashboard](docs/screenshots/dashboard.png)

### Device Management
![Device Management](docs/screenshots/device-manager.png)

### Reports
![Reports](docs/screenshots/reports.png)

---

## 🗂️ Project Structure

```
EnergyMonitor/
├── EnergyMonitor.Interface/      # Models & Interfaces
├── EnergyMonitor.SP/              # Data Access (Dapper)
├── EnergyMonitor.Business/        # Business Logic
├── EnergyMonitor.Service/         # MQTT, AI, External Services
├── EnergyMonitor.Forms/           # WinForms UI
├── EnergyMonitor.Launcher/        # Application Entry Point
├── EnergyMonitor.Api/             # REST API
├── MockEsp32/                     # ESP32 Simulator for Testing
├── schema_v2.sql                  # Database Schema
└── esp32_firmware_persistence.ino # ESP32 Firmware
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔮 Roadmap

### Short-term (1-3 months)
- [ ] Multi-tenant support
- [ ] Real-time alarm system
- [ ] Mobile app (React Native)
- [ ] TLS/SSL for MQTT

### Mid-term (3-6 months)
- [ ] LSTM-based advanced prediction models
- [ ] Anomaly detection (Isolation Forest)
- [ ] Cloud integration (Azure/AWS)
- [ ] RESTful API expansion

### Long-term (6-12 months)
- [ ] ISO 50001 certification support
- [ ] Blockchain-based data verification
- [ ] Digital Twin integration
- [ ] Kubernetes deployment

---

## 📚 Documentation

- [Academic Report](docs/akademik_rapor.md) (Turkish)
- [Technical Reference](docs/teknik_referans.md) (Turkish)
- [UML Diagrams](docs/uml_diagrams.md)
- [API Documentation](docs/api.md)

---

## 🙏 Acknowledgments

- **Google Gemini API** for AI-powered recommendations
- **DevExpress** for UI components
- **Eclipse Mosquitto** for MQTT broker
- **PostgreSQL** for robust database management
- **Espressif Systems** for ESP32 platform

---

## 📧 Contact

**Umut Zaif**
- GitHub: [@umutzaif](https://github.com/umutzaif)
- Project Link: [Enerlytics-Factory-Energy-Viewer](https://github.com/umutzaif/Enerlytics-Factory-Energy-Viewer)

---

<div align="center">
  <strong>⭐ If you find this project useful, please consider giving it a star! ⭐</strong>
</div>
