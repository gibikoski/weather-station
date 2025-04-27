# Tabela de Dependências - Projeto Estação Meteorológica

## Bibliotecas Arduino
| **Biblioteca** | **Versão Sugerida** | **Componente** | **Fonte** | **Notas** |
| --- | --- | --- | --- | --- |
| Adafruit_BME280 | ~2.2.2 | BME280 (Temperatura, Umidade, Pressão) | [GitHub](https://github.com/adafruit/Adafruit_BME280_Library) | I2C, endereço 0x76/0x77. |
| Adafruit_SHT31 | ~1.0.0 | SHT31 (Temperatura, Umidade) | [GitHub](https://github.com/adafruit/Adafruit_SHT31) | I2C, endereço 0x44/0x45. |
| Adafruit_SI1145 | ~1.0.0 | SI1145 (Radiação Solar, UV) | [GitHub](https://github.com/adafruit/Adafruit_SI1145_Library) | I2C, endereço 0x60. |
| PMS | ~1.1.0 | PMS5003 (PM2.5) | [GitHub](https://github.com/fu-hsi/pms) | UART, GPIO 20, 21. |
| RTClib | ~2.1.4 | DS3231 (RTC) | [GitHub](https://github.com/adafruit/RTClib) | I2C, wake-up para deep sleep. |
| Adafruit_INA219 | ~1.2.0 | INA219 (Tensão/Corrente) | [GitHub](https://github.com/adafruit/Adafruit_INA219) | I2C, 0-6 V, 0-600 mA. |
| Arduino | ~2.3.2 | ESP32-C3 (Core) | [ESP32 Arduino](https://github.com/espressif/arduino-esp32) | Suporte a Wi-Fi, MQTT, ESP-NOW. |

## Notas
- Versões sugeridas são estáveis em 27/04/2025. Verificar atualizações antes de usar.
- Instalar via Arduino IDE (Library Manager) ou manualmente (GitHub).
- Testar compatibilidade com ESP32-C3 (ex.: I2C, UART, deep sleep).
