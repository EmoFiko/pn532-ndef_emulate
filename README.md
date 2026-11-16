# PN532 Rickroll NDEF Emulator

ESP32 ve PN532 NFC modülü ile telefonuna **NDEF etiketi** gibi görünen bir cihaz yap. Telefonu PN532'ye yaklaştırdığında ekranda bir YouTube linki (Rickroll) çıkar.

## İçerik

- `src/main.cpp` — ESP32 ana kodu (NDEF emülasyonu + seri komutlar)
- `lib/PN532/` — PN532 sürücüsü ve `EmulateTag` sınıfı
- `lib/NDEF/` — NDEF mesaj oluşturma kütüphanesi
- `platformio.ini` — PlatformIO proje ayarları

## Donanım

- ESP32 geliştirme kartı
- PN532 NFC modülü (HSU/UART modu)
- 4 adet dupont kablo

## Bağlantı

| PN532 | ESP32 |
|-------|-------|
| TX | GPIO 16 (RX2) |
| RX | GPIO 17 (TX2) |
| GND | GND |
| VCC | 3.3V (veya 5V) |

**DIP switchleri:** OFF – OFF (HSU modu)

## Kurulum

1. Depoyu bilgisayara indir veya klonla.
2. Klasörü **PlatformIO IDE** (VS Code) ile aç.
3. ESP32'yi bilgisayara bağla.
4. Terminalde şu komutu çalıştır (portunu kendi portunla değiştir, ör. COM3, COM6):

```bash
pio run -t upload --upload-port COM6
```

5. Arduino IDE Serial Monitor'u aç, baud rate'i **9600** yap.

## Kullanım

1. Serial Monitor'a **`E`** yazıp **Gönder**'e bas.
2. Telefonunu **PN532 anteninin üzerine sıkmak ve basılı tut**.
3. Telefon ekranında bir NDEF etiketi çıkacak ve link açılacaktır.

> Bazı Android telefonları linki otomatik tarayıcıda açmaz. NFC Tools gibi bir uygulama ile kaydı görebilir, linki elle tıklayabilirsin.

## Seri Komutlar

| Komut | Açıklama |
|-------|----------|
| `E` | NDEF Rickroll emülasyonunu başlat |
| `R` | Yakındaki MIFARE kartı oku |
| `L` | Kaydedilmiş kartları listele |
| `W0` | ID 0'lı kaydı başka bir karta klonla |
| `D0` | ID 0'lı kaydı sil |

## Not

Bu proje PN532'nin ISO 14443-4 (Type 4) NDEF emülasyonunu kullanır. Telefonun NFC'si açık olmalı ve PN532 antenine sıkmak gerekebilir.

---

## Kaynak ve Teşekkür

Bu proje [SudeKun/NFC_Wallet_Project](https://github.com/SudeKun/NFC_Wallet_Project) üzerinden yapılmıştır. Orijinal repodaki PN532 ve NDEF kütüphanelerinden yararlanılmıştır.
