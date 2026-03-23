# ScanCI Backend 🔲

> **"Scan"** + **CI** — Référence directe au QR code et au Mobile Money (Orange Money, Wave, MTN) très utilisé en Côte d'Ivoire.

**Challenge 14-14-14 — Jour 10 — Mars 2026**

---

## 📋 Aperçu

ScanCI Backend est l'API REST du générateur de QR codes ScanCI. Elle gère l'authentification des utilisateurs, la génération de QR codes via ZXing et l'historique des QR codes générés.

---

## ✨ Fonctionnalités

- 🔐 **Authentification JWT** — register, login, token refresh
- 🔲 **Génération QR** — 5 types supportés via ZXing
- 🎨 **Personnalisation** — couleurs foreground/background, taille, correction d'erreur
- 📥 **Export** — PNG (base64) + SVG
- 🕐 **Historique** — sauvegarde et récupération par utilisateur
- 🗑️ **Suppression** — suppression d'un QR code de l'historique
- 🛡️ **Sécurité** — Spring Security + JWT filter

---

## 🛠️ Stack technique

| Couche | Technologie |
|---|---|
| Framework | Spring Boot 3.x |
| Langage | Java 17 |
| Sécurité | Spring Security + JWT |
| Génération QR | ZXing (Google) |
| Base de données | PostgreSQL |
| ORM | Spring Data JPA |
| Build | Maven |

---

## 🏗️ Architecture
```
src/main/java/ci/jinx/qr_code/
├── auth/
│   ├── AuthController.java        → POST /auth/login, /auth/register
│   ├── AuthService.java           → Logique authentification
│   └── dto/
│       ├── AuthResponse.java      → Token JWT retourné
│       ├── LoginRequest.java      → Email + password
│       └── RegisterRequest.java   → Name + email + password
├── config/
│   ├── JwtAuthFilter.java         → Filtre JWT sur chaque requête
│   ├── JwtService.java            → Génération et validation du token
│   └── SecurityConfig.java        → Configuration Spring Security
├── models/
│   ├── User.java                  → Entité utilisateur
│   ├── QrCode.java                → Entité QR code
│   └── QrCodeType.java            → Entité type de QR code
├── qrcode/
│   ├── QrCodeController.java      → Endpoints QR codes
│   ├── QrCodeService.java         → Logique génération ZXing
│   └── dto/
│       ├── QrCodeRequest.java     → Paramètres de génération
│       ├── QrCodeResponse.java    → QR code généré (base64 + SVG)
│       └── content/
│           ├── UrlContent.java    → Contenu URL
│           ├── TextContent.java   → Contenu texte
│           ├── EmailContent.java  → Contenu email
│           ├── WifiContent.java   → Contenu WiFi
│           └── VCardContent.java  → Contenu vCard
└── repository/
    ├── UserRepository.java
    ├── QrCodeRepository.java
    └── QrCodeTypeRepository.java
```

---

## 🌐 Endpoints API

### Auth

| Endpoint | Méthode | Auth | Description |
|---|---|---|---|
| `/auth/register` | POST | ❌ | Créer un compte |
| `/auth/login` | POST | ❌ | Se connecter |

### QR Codes

| Endpoint | Méthode | Auth | Description |
|---|---|---|---|
| `/qr-codes/generate` | POST | ✅ | Générer un QR code |
| `/qr-codes/types` | GET | ✅ | Liste des types |
| `/qr-codes/history` | GET | ✅ | Historique utilisateur |
| `/qr-codes/:id` | DELETE | ✅ | Supprimer un QR code |

---

## 📝 Exemples de requêtes

### Register
```json
POST /auth/register
{
  "name": "Kouame Aya",
  "email": "aya@225os.com",
  "password": "motdepasse123"
}
```

### Générer un QR code URL
```json
POST /qr-codes/generate
Authorization: Bearer <token>
{
  "contentType": "URL",
  "contentData": { "url": "https://225os.com" },
  "foregroundColor": "#FF8C00",
  "backgroundColor": "#FFFFFF",
  "size": 512
}
```

### Générer un QR code WiFi
```json
POST /qr-codes/generate
Authorization: Bearer <token>
{
  "contentType": "WIFI",
  "contentData": {
    "ssid": "MonReseau",
    "password": "motdepasse",
    "security": "WPA"
  },
  "foregroundColor": "#000000",
  "backgroundColor": "#FFFFFF",
  "size": 300
}
```

---

## 🚀 Installation

### Prérequis

- Java 17+
- Maven 3.8+
- PostgreSQL 14+

### Configuration `application.properties`
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/scanci
spring.datasource.username=postgres
spring.datasource.password=tonmotdepasse
spring.jpa.hibernate.ddl-auto=update
jwt.secret=TON_SECRET_JWT
jwt.expiration=86400000
```

### Lancer le projet
```bash
# Cloner le repo
git clone https://github.com/bath01/14challenge-scanci-backend.git
cd 14challenge-scanci-backend

# Build
mvn clean install

# Lancer
mvn spring-boot:run
```

L'API sera disponible sur `http://localhost:8080`

---

## 👥 Équipe

| Nom | Rôle |
|---|---|
| Bath Dorgeles | Chef de projet & Front-end |
| Oclin Marcel C. | Dev Front-end (Angular) |
| Rayane Irie | Back-end (Spring Boot) |

---

## 📄 Licence

Open Source · [225os.com](https://225os.com) & [GitHub](https://github.com/bath01)

---

*14-14-14 // JOUR 10 // MARS 2026*