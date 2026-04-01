
<div align="center">
  
# ⚡ SINOTIMER SVP-688W
  
## ESPHome Edition · Smart Circuit Breaker

</div>

---

<div align="center">

### **Умный автоматический выключатель, который говорит на языке Home Assistant**

**63A защиты · 16 активных датчиков · 6 уровней безопасности · 0 строк кода для интеграции**

[![ESPHome](https://img.shields.io/badge/ESPHome-2024.12.0-000000?logo=esphome&style=flat-square)](https://esphome.io)
[![Buy me a coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-donate-FFDD00?style=flat-square&logo=buy-me-a-coffee)](https://buymeacoffee.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/yourusername/sinotimer-esphome?style=flat-square)](https://github.com/yourusername/sinotimer-esphome/stargazers)
[![ESP8266](https://img.shields.io/badge/ESP8266-12E-blue?style=flat-square)](https://www.espressif.com)

</div>

---

## 🎯 **Ваша умная сеть теперь под полным контролем**

Представьте: вы больше не бежите к щитку, когда щёлкает реле. **SINOTIMER SVP-688W** превращается в полноценного члена вашей умной семьи — с мониторингом в реальном времени, настраиваемыми защитами и голосовым управлением через Алису или Google Assistant.

Этот конфиг — не просто прошивка. Это **взлом безопасности** в хорошем смысле. Мы вытащили все 20+ скрытых датапоинтов Tuya и превратили обычный автомат в **интеллектуальный центр управления энергопотреблением**.

---

## 📸 **Как это выглядит**

> *Вот так ваш Home Assistant увидит SINOTIMER после первой прошивки:*


⚡ Что умеет эта прошивка
<table> <tr> <td width="33%"> <h3>🔍 <strong>Мониторинг 24/7</strong></h3> <ul> <li>Напряжение, ток, мощность — с точностью до 0.1V и 1mA</li> <li>4 вида счётчиков энергии: общий, обратный, баланс, заряд</li> <li>WiFi Signal, Uptime, IP — всё под рукой</li> </ul> </td> <td width="33%"> <h3>🛡️ <strong>6 уровней защиты</strong></h3> <ul> <li>Ток утечки (10-99 mA)</li> <li>Перегруз по току (1-63A)</li> <li>Перенапряжение / Пониженное напряжение</li> <li>Температурная защита (10-85°C)</li> <li>Автоматическое повторное включение</li> <li>Диагностика 20+ типов аварий</li> </ul> </td> <td width="33%"> <h3>🎮 <strong>Полный контроль</strong></h3> <ul> <li>Веб-интерфейс ESPHome</li> <li>Управление через Home Assistant</li> <li>Автоматизации по любым параметрам</li> <li>Предоплатный режим (для аренды)</li> </ul> </td> </tr> </table>

## 🚀 **Быстрый старт за 5 минут**

### 1️⃣ Подготовка
```bash
# Установите ESPHome (если ещё не сделали)
pip install esphome

# Клонируйте репозиторий
git clone https://github.com/yourusername/sinotimer-esphome.git
cd sinotimer-esphome
```

2️⃣ Настройка
```yaml
# Создайте файл secrets.yaml в той же папке
wifi_ssid: "Ваш WiFi"
wifi_password: "Ваш пароль"
wifi_ssid2: "Резервная сеть"  # опционально
wifi_password2: "Резервный пароль"
```

3️⃣ Прошивка
```bash
# Подключите SINOTIMER через USB-UART (3.3V!)
esphome run sinotimer-smart-ac_actual_config_1.yaml
```

4️⃣ Первое включение
После прошивки устройство создаст точку доступа Sinotimer svp-688w Hotspot

Пароль: 

Подключитесь и введите ваши WiFi-данные

Готово! 🎉 Ваш автомат появится в Home Assistant через интеграцию ESPHome автоматически.

## 🏗️ **Архитектура: как это работает**

```mermaid
graph LR
    subgraph "🔌 Устройство"
        direction TB
        A[<b>ESP8266</b><br/>+ Tuya MCU] --> B[<b>UART</b><br/>9600 baud]
        B --> C[<b>Декодинг</b><br/>DP 6,9,17,18...]
        C --> D[<b>Template</b><br/>Sensors]
        D --> E[<b>ESPHome</b><br/>API]
    end
    
    subgraph "🏠 Домашняя автоматизация"
        direction TB
        E --> F[<b>Home</b><br/><b>Assistant</b>]
        E --> G[<b>Веб-интерфейс</b><br/>:80]
        F --> H[🤖 <b>Автоматизации</b><br/>Сценарии]
        F --> I[💬 <b>Уведомления</b><br/>Telegram / Алиса]
    end
    
    subgraph "🛡️ Система защиты"
        direction TB
        J[<b>Пороги</b><br/>срабатывания] --> K[<b>Tuya</b><br/>Commands]
        K --> L[<b>Аппаратное</b><br/>отключение]
    end
    
    style A fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style C fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style D fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style E fill:#c8e6c9,stroke:#1b5e20,stroke-width:2px
    style F fill:#c8e6c9,stroke:#1b5e20,stroke-width:2px
    style G fill:#c8e6c9,stroke:#1b5e20,stroke-width:2px
    style H fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    style I fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    style J fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style K fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style L fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
```


    Магия в деталях:

DP6 передаёт напряжение/ток/мощность одним пакетом

DP9 — битовая маска из 20 типов аварий

Все защиты настраиваются через Home Assistant и сохраняются в энергонезависимой памяти


